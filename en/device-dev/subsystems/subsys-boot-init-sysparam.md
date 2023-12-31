# Parameter Management

## Overview

### Function

The parameter management subsystem, namely, sysparam, provides easy-to-use key-value pair access interfaces for system services to customize functions based on their own system parameters.

### Basic Concepts

#### Operation Primitives

Figure 1 shows the primitives used to operate system parameters. For details about how they work, see Table 1.

Figure 1 Overview of system parameter operation primitives

![System parameter operation primitives](figures/system-parameter-operation-primitives.png)

**Table 1** Description of system parameter operation primitives

| Operation Primitive | Description |
| -------- | -------- |
| get      | Obtains the value of a system parameter.       |
| set      | Sets the value of a system parameter.       |
| wait     | Waits for value change of a system parameter synchronously.|
| watch    | Watches for the value change of a system parameter asynchronously.|

#### Parameter Definition

- Naming format

  A system parameter name consists of multiple segments in dotted notation. Each segment can be a string that consists of letters, digits, and underscores (_). The total length cannot exceed 96 bytes. 

  Two naming formats are supported for system parameters, as described in Table 2.

  **Table 2** Description of system parameter naming formats

  | Type | Example | Description |
  | -------- | -------- | -------- |
  | Parameter name | const.product.**name** | Complete system parameter name. It does not end with a period (.).          |
  | Parameter directory | const.product **.**     | Name of the directory storing system parameters with the same prefix. It ends with a period (.).|

- Type

  System parameters are categorized into three types, as described in Table 3.

  **Table 3** Description of system parameter types

  | Type| Prefix| Description|
  | -------- | -------- | -------- |
  | Constant| const. | Constant parameter, which will not change once a value is assigned. The value can contain a maximum of 4,096 bytes (including the end-of-text character).|
  | Writable| Others| Writable parameter, which will be discarded after a system restart. The value can contain a maximum of 96 bytes (including the end-of-text character).|
  | Persistent| persist. | Writable and persistent parameter, which will not be discarded after a system restart. The value can contain a maximum of 96 bytes (including the end-of-text character).|

  Given below is the general naming format for system parameters:
  ```
  [ const | persist ].$sub_system.$desc
  ```
  wherein,
  
  - **$sub_system** is the subsystem or module name.

  - **$desc** is the parameter description, which can contain multiple segments in dotted notation.

#### Parameter Definition Rule

System parameters are defined per module on each subsystem. The parameter definition includes the system parameter name, default value, and access permission information.

- Value definition file

  - A value definition file of system parameters ends with the **.para** extension. The following is an example format of file content:

    ```shell
    # This is comment
    const.product.name=OHOS-PRODUCT
    const.os.version.api=26
    const.telephony.enable=false|true

    const.test.withblank=My Value
    const.test.withcomment=MyValue # This should be omitted
    const.test.multiline="This is a multiline parameter.
    Line2 value.
    Last line."
    ```

  - A complete system parameter command is required to assign a value for a system parameter. See Table 4 for the value assignment modes.

    **Table 4** Description of value assignment modes

    | Type| Example| Description|
    | -------- | -------- | -------- |
    | String  | const.product.name=OHOS-PRODUCT | A string that spans multiple lines must be enclosed in double quotation marks ("").|
    | Number    | const.os.version.api=26         | A number that spans multiple lines does not need to be enclosed in double quotation marks ("").|
    | Boolean    | const.telephony.enable=false    | A Boolean value can be **0**, **1**, **false**, or **true**.|

- DAC definition file

  Access permissions of system parameters are managed in discretionary access control (DAC) mode. A DAC definition file ends with the **.para.dac** extension. The following is an example format of DAC information:

  ```java
  const.product.="root:root:660"
  ```

  As shown in this example, a **parameter directory** can be used to define the same access permission for system parameters with the same prefix. A piece of DAC information is divided into three segments, user, group, and Ugo rule, which are separated using a semicolon (:).

  > **NOTE**
  > 
  > Ugo is the abbreviation for user access, group access, ad other system user's access, respectively. These permissions are set to allow or deny access to members of their own group, or any other groups.

  Figure 2 shows the Ugo rule structure.

  **Figure 2** Overview of the Ugo rule structure

  ![Ugo rule](figures/dac-definition.png)

- SELinux policy

  An SELinux policy defines the access permissions for all users, programs, processes, and files.

  - Adding an SELinux tag

    To add an SELinux tag to system parameters, you first need to define the tag in the **/base/security/selinux/sepolicy/base/public/parameter.te** file. For example:

    ```java
    type servicectrl_param, parameter_attr
    ```

    After the tag is defined, add the system parameter prefix associated with the tag to **/base/security/selinux/sepolicy/base/public/parameter_contexts**. The following uses the prefix **ohos.servicectrl** as an example:

    ```java
    ohos.servicectrl.           u:object_r:servicectrl_param:s0
    ```

  - Granting access permissions for a process

    For example, to grant access permissions such as map for the init process, add the following code to the **/base/security/selinux/sepolicy/ohos_policy/startup/init/public/init.te** file:

    ```java
    allow servicectrl_param tmpfs:filesystem associate;
    allow init servicectrl_param:file { map open read relabelto relabelfrom };
    ```

  - Granting the write permission

    For example, to grant the write permission for services such as **init**, **samgr**, and **hdf_devmgr**, use the following code:

    ```java
    allow { init samgr hdf_devmgr } servicectrl_param:parameter_service { set };
    ```

  - Granting the read permission

    If you want to grant the read permission only for certain services, replace **xxx** with these services in the following code:

    ```java
    allow { xxx } servicectrl_param:file { map open read };
    ```

  - Granting access permissions for all services

    If you want to grant access permissions for all services, use the following code:

    ```java
    allow { domain -limit_domain } servicectrl_param:file { map open read };
    ```

-  System parameter tag

   You are advised to keep only two system parameter tags for each subsystem:

   - A private tag to control system parameter settings.

   - A public tag to grant access permissions from all services.

-  Loading sequence

   System parameters are loaded by priority in the specified sequence, as described in Table 5.

    **Table 5** Description of the system parameter loading sequence

    | Type| Path| Description|
    | -------- | -------- | -------- |
    | Kernel parameters   | /proc/cmdline | Convert some values of kernel parameters into system parameters. Specifically, convert all **ohospara.xxx=valXXX** parameters to **ohos.boot.xxx=valXXX** parameters.|
    | OS system parameters| /system/etc/param/ohos_const/*.para | Load the definition file containing OS constants preferentially.                              |
    | Vendor parameters| /vendor/etc/param/*.para | Load the system parameters defined by vendors with the secondary priority.                            |
    | System parameters| /system/etc/param/*.para | Load the system parameters defined by each subsystem. A system parameter will be ignored if it already exists.|
    | Persistent parameters| /data/parameters/ | Load persistent parameters, if any, at last. Persistent parameters will overwrite the default system parameters that have been loaded.|


#### Tag File Size

If one tag is associated with more than five system parameters, you need to set the size of the system parameter tag file in **/base/startup/init/services/etc/param/ohos.para.size**. The default value is **512**.

The configuration rule is as follows:

System parameter tag = Size

For example:

```java
startup_init_param=40960
```


### Constraints

The parameter management subsystem is available only for the mini system and standard system.

## How to Develop

### Application Scenario

You can set specific system parameters as needed to meet your service demand.

### Implementation Method

The parameter management subsystem allows you to manage system parameters by running shell commands or calling **syspara** APIs.

  - Shell command mode

    You can operate system parameters directly by running shell commands. This operation mode is available only for the standard system. Table 6 is a list of the shell commands.

    **Table 6** Description of shell commands

    | Command| Description|
    | -------- | -------- |
    | param get [**key**] | Obtains the system parameter value of the specified key. If no key name is specified, all system parameter values will be returned.|
    | param set **key value** | Sets the specified value for the specified key.|
    | param wait **key** **value** | Waits for the system parameter value of the specified key to match the specified value. Fuzzy match is supported. For example, * indicates any value, and <strong>val</strong>* indicates matching of only the first three val characters.|
    | param watch | Watches for the value change of a system parameter asynchronously.|

  - syspara API mode

    Besides shell commands, you can use **syspara** APIs to manage system parameters. The return result is a constant string and the **free** operation is not supported. Table 7 is a list of the **syspara** APIs. 

    **Table 7** Description of syspara APIs

    | API| Description|
    | -------- | -------- |
    | int&nbsp;GetParameter(const&nbsp;char\*&nbsp;key,&nbsp;const&nbsp;char\*&nbsp;def,&nbsp;char\*&nbsp;value,&nbsp;unsigned&nbsp;int&nbsp;len) | Obtains system parameters.|
    | int&nbsp;SetParameter(const&nbsp;char\*&nbsp;key,&nbsp;const&nbsp;char\*&nbsp;value) | Sets or updates system parameters.|
    | const&nbsp;char\*&nbsp;GetDeviceType(void) | Obtains the device type.|
    | const&nbsp;char\*&nbsp;GetManufacture(void) | Obtains the device's manufacturer name.|
    | const&nbsp;char\*&nbsp;GetBrand(void) | Obtains the device's brand name.|
    | const&nbsp;char\*&nbsp;GetMarketName(void) | Obtains the device's marketing name.|
    | const&nbsp;char\*&nbsp;GetProductSeries(void) | Obtains the device's product series name.|
    | const&nbsp;char\*&nbsp;GetProductModel(void) | Obtains the device's product model.|
    | const&nbsp;char\*&nbsp;GetSoftwareModel(void) | Obtains the device's software model.|
    | const&nbsp;char\*&nbsp;GetHardwareModel(void) | Obtains the device's hardware model.|
    | const&nbsp;char\*&nbsp;GetHardwareProfile(void) | Obtains the device's hardware profile.|
    | const&nbsp;char\*&nbsp;GetSerial(void) | Obtains the device's serial number (SN).|
    | const&nbsp;char\*&nbsp;GetOSFullName(void) | Obtains the device's OS name.|
    | const&nbsp;char\*&nbsp;GetDisplayVersion(void) | Obtains the device's displayed software version.|
    | const&nbsp;char\*&nbsp;GetBootloaderVersion(void) | Obtains the device's bootloader version.|
    | const&nbsp;char\*&nbsp;GetSecurityPatchTag(void) | Obtains the device's security patch tag.|
    | const&nbsp;char\*&nbsp;GetAbiList(void) | Obtains the list of supported application binary interfaces (ABIs).|
    | int&nbsp;GetSdkApiVersion(void) | Obtains the SDK API version that matches the current system software.|
    | int&nbsp;GetFirstApiVersion(void) | Obtains the first SDK API version of the system software.|
    | const&nbsp;char\*&nbsp;GetIncrementalVersion(void) | Obtains the incremental version of the system software.|
    | const&nbsp;char\*&nbsp;GetVersionId(void) | Obtains the version ID.|
    | const&nbsp;char\*&nbsp;GetBuildType(void) | Obtains the build type.|
    | const&nbsp;char\*&nbsp;GetBuildUser(void) | Obtains the build user.|
    | const&nbsp;char\*&nbsp;GetBuildHost(void) | Obtains the build host.|
    | const&nbsp;char\*&nbsp;GetBuildTime(void) | Obtains the build time.|
    | const&nbsp;char\*&nbsp;GetBuildRootHash(void) | Obtains the buildroot hash value of the current version.|
    | const&nbsp;char\*&nbsp;GetOsReleaseType(void) | Obtains the system release type.|
    | int&nbsp;GetDevUdid(char&nbsp;\*udid,&nbsp;int&nbsp;size) | Obtains the device's unique device ID (UDID).|
    | const char *AclGetSerial(void); | Obtains the device's SN with ACL check.|
    | int AclGetDevUdid(char *udid, int size); | Obtains the device's UDID with ACL check.|

### Development Procedure

#### Parameter Definition

You can define default system parameters and implement permission control on them by configuring the <strong>.para</strong> and <strong>.para.dac</strong> files of the respective subsystem or product.

- On a standard system, use the <strong>ohos_prebuilt_para</strong> template to install the configuration file to the <strong>/etc/param/</strong> directory. The following is an example of the GN script:

    ```go
    import("//base/startup/init/services/etc/param/param_fixer.gni")

    ohos_prebuilt_para("ohos.para") {
        source = "//base/startup/init/services/etc/ohos.para"
        part_name = "init"
        module_install_dir = "etc/param"
    }

    ohos_prebuilt_para("ohos.para.dac") {
        source = "//base/startup/init/services/etc/ohos.para.dac"
        part_name = "init"
        module_install_dir = "etc/param"
    }
    ```

- On a small system, run the <strong>copy</strong> command to copy the corresponding system parameter definition file to the <strong>system/etc/param</strong> directory.
    ```go
    copy("ohos.para") {
      sources = [ "//base/startup/init/services/etc/param/ohos.para" ]
      outputs = [ "$root_out_dir/system/etc/param/ohos.para" ]
    }
    copy("ohos.para.dac") {
      sources = [ "//base/startup/init/services/etc/param/ohos.para.dac" ]
      outputs = [ "$root_out_dir/system/etc/param/ohos.para.dac" ]
    }
    ```
- On a mini system, convert all defined default system parameters into header files through **action** and compile them into the system.
    ```go
    action("lite_const_param_to") {
      script = "//base/startup/init/scripts/param_cfg_to_code.py"
      args = [
        "--source",
        rebase_path(
            "//base/startup/init/services/etc_lite/param/ohos_const/ohospara"),
        "--dest_dir",
        rebase_path("$root_out_dir/gen/init/"),
        "--priority",
        "0",
      ]
      outputs = [ "$target_gen_dir/${target_name}_param_cfg_to_code.log" ]
    }
    ```
#### Development Example
    ```
    // set && get
    char key1[] = "rw.sys.version";
    char value1[] = "10.1.0";
    int ret = SetParameter(key1, value1);
    char valueGet1[128] = {0};
    ret = GetParameter(key1, "version=10.1.0", valueGet1, 128);

    // get sysparm
    char* value1 = GetDeviceType();
    printf("Product type =%s\n", value1);

    char* value2 = GetManufacture();
    printf("Manufacture =%s\n", value2);

    char* value3 = GetBrand();
    printf("GetBrand =%s\n", value3);

    char* value4 = GetMarketName();
    printf("MarketName =%s\n", value4);

    char* value5 = GetProductSeries();
    printf("ProductSeries =%s\n", value5);

    char* value6 = GetProductModel();
    printf("ProductModel =%s\n", value6);

    char* value7 = GetSoftwareModel();
    printf("SoftwareModel =%s\n", value7);

    char* value8 = GetHardwareModel();
    printf("HardwareModel =%s\n", value8);

    char* value9 = GetHardwareProfile();
    printf("Software profile =%s\n", value9);

    char* value10 = GetSerial();
    printf("Serial =%s\n", value10);

    char* value11 = GetOSFullName();
    printf("OS name =%s\n", value11);

    char* value12 = GetDisplayVersion();
    printf("Display version =%s\n", value12);

    char* value13 = GetBootloaderVersion();
    printf("bootloader version =%s\n", value13);

    char* value14 = GetSecurityPatchTag();
    printf("secure patch level =%s\n", value14);

    char* value15 = GetAbiList();
    printf("abi list =%s\n", value15);

    int value16 = GetFirstApiVersion();
    printf("first api level =%d\n", value16);

    char* value17 = GetIncrementalVersion();
    printf("Incremental version = %s\n", value17);

    char* value18 = GetVersionId();
    printf("formal id =%s\n", value18);

    char* value19 = GetBuildType();
    printf("build type =%s\n", value19);

    char* value20 = GetBuildUser();
    printf("build user =%s\n", value20);

    char* value21 = GetBuildHost();
    printf("Build host = %s\n", value21);

    char* value22 = GetBuildTime();
    printf("build time =%s\n", value22);

    char* value23 = GetBuildRootHash();
    printf("build root later..., %s\n", value23);

    char* value24 = GetOsReleaseType();
    printf("OS release type =%s\n", value24);

    char* value25 = GetOsReleaseType();
    printf("OS release type =%s\n", value25);

    char value26[65] = {0};
    GetDevUdid(value26, 65);
    printf("device udid =%s\n", value26);
    ```
