| Change Type | Old Version | New Version | d.ts File |
| ---- | ------ | ------ | -------- |
|Added|NA|Class name: Authenticator<br>Method or attribute name: checkAccountRemovable(name: string, callback: AuthCallback): void;|@ohos.account.appAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: checkOsAccountConstraintEnabled(localId: number, constraint: string, callback: AsyncCallback\<boolean>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: checkOsAccountConstraintEnabled(localId: number, constraint: string): Promise\<boolean>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalId(callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalId(): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForUid(uid: number, callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForUid(uid: number): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForDomain(domainInfo: DomainAccountInfo, callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForDomain(domainInfo: DomainAccountInfo): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getActivatedOsAccountLocalIds(callback: AsyncCallback\<Array\<number>>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getActivatedOsAccountLocalIds(): Promise\<Array\<number>>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForSerialNumber(serialNumber: number, callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountLocalIdForSerialNumber(serialNumber: number): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getSerialNumberForOsAccountLocalId(localId: number, callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getSerialNumberForOsAccountLocalId(localId: number): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getBundleIdForUid(uid: number, callback: AsyncCallback\<number>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getBundleIdForUid(uid: number): Promise\<number>;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountConstraintSourceTypes(localId: number, constraint: string, callback: AsyncCallback\<Array\<ConstraintSourceTypeInfo>>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager<br>Method or attribute name: getOsAccountConstraintSourceTypes(localId: number, constraint: string): Promise\<Array\<ConstraintSourceTypeInfo>>;|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.appAccount<br>Class name: OAuthTokenInfo<br>Method or attribute name: account?: AppAccountInfo;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Module name: ohos.account.appAccount<br>Class name: AuthenticatorCallback<br>Method or attribute name: onRequestContinued?: () => void;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Module name: ohos.account.appAccount<br>Class name: Authenticator<br>Method or attribute name: isAccountRemovable(name: string, callback: AuthCallback): void;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: checkConstraintEnabled(localId: number, constraint: string, callback: AsyncCallback\<boolean>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: checkConstraintEnabled(localId: number, constraint: string): Promise\<boolean>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromProcess(callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromProcess(): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromUid(uid: number, callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromUid(uid: number): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromDomain(domainInfo: DomainAccountInfo, callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdFromDomain(domainInfo: DomainAccountInfo): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: getActivatedOsAccountIds(callback: AsyncCallback\<Array\<number>>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: getActivatedOsAccountIds(): Promise\<Array\<number>>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdBySerialNumber(serialNumber: number, callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountLocalIdBySerialNumber(serialNumber: number): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: querySerialNumberByOsAccountLocalId(localId: number, callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: querySerialNumberByOsAccountLocalId(localId: number): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: getBundleIdFromUid(uid: number, callback: AsyncCallback\<number>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: getBundleIdFromUid(uid: number): Promise\<number>;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountConstraintSourceTypes(localId: number, constraint: string, callback: AsyncCallback\<Array\<ConstraintSourceTypeInfo>>): void;|NA|@ohos.account.osAccount.d.ts|
|Deleted|Module name: ohos.account.osAccount<br>Class name: AccountManager<br>Method or attribute name: queryOsAccountConstraintSourceTypes(localId: number, constraint: string): Promise\<Array\<ConstraintSourceTypeInfo>>;|NA|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_NOT_EXIST = 0<br>Initial version: N/A|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_NOT_EXIST = 0<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_BASE = 1<br>Initial version: N/A|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_BASE = 1<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_DEVICE_OWNER = 2<br>Initial version: N/A|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_DEVICE_OWNER = 2<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_PROFILE_OWNER = 3<br>Initial version: N/A|Class name: ConstraintSourceType<br>Method or attribute name: CONSTRAINT_TYPE_PROFILE_OWNER = 3<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceTypeInfo<br>Method or attribute name: localId: number;<br>Initial version: N/A|Class name: ConstraintSourceTypeInfo<br>Method or attribute name: localId: number;<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Initial version changed|Class name: ConstraintSourceTypeInfo<br>Method or attribute name: type: ConstraintSourceType;<br>Initial version: N/A|Class name: ConstraintSourceTypeInfo<br>Method or attribute name: type: ConstraintSourceType;<br>Initial version: 9|@ohos.account.osAccount.d.ts|
|Permission deleted|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(callback: AsyncCallback\<boolean>): void;<br>Permission: ohos.permission.MANAGE_LOCAL_ACCOUNTS or ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(callback: AsyncCallback\<boolean>): void;<br>Permission: N/A|@ohos.account.osAccount.d.ts|
|Error code added|NA|Class name: PINAuth<br>Method or attribute name: unregisterInputer(): void;<br>Error code: 201|@ohos.account.osAccount.d.ts|
|Error code added|NA|Class name: UserIdentityManager<br>Method or attribute name: closeSession(): void;<br>Error code: 201|@ohos.account.osAccount.d.ts|
|Function changed|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(localId?: number): Promise\<boolean>;<br>|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(): Promise\<boolean>;<br>|@ohos.account.osAccount.d.ts|
|Function changed|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(localId?: number): Promise\<boolean>;<br>|Class name: AccountManager<br>Method or attribute name: checkOsAccountVerified(localId: number): Promise\<boolean>;<br>|@ohos.account.osAccount.d.ts|
|Function changed|Class name: IInputData<br>Method or attribute name: onSetData: (pinSubType: AuthSubType, data: Uint8Array) => void;<br>|Class name: IInputData<br>Method or attribute name: onSetData: (authSubType: AuthSubType, data: Uint8Array) => void;<br>|@ohos.account.osAccount.d.ts|
|Function changed|Class name: IInputer<br>Method or attribute name: onGetData: (pinSubType: AuthSubType, callback: IInputData) => void;<br>|Class name: IInputer<br>Method or attribute name: onGetData: (authSubType: AuthSubType, callback: IInputData) => void;<br>|@ohos.account.osAccount.d.ts|