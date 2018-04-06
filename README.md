# ActiveDirectoryCSDsc

The **ActiveDirectoryCSDsc** DSC resources have been specifically tested as a method
to populate a Certificate Services server role on Windows Server 2012 R2 and above
after the Certificate Services role and the Web Enrollment feature have been enabled.
Active Directory Certificate Services (AD CS) is used to create certification
authorities and related role services that allow you to issue and manage certificates
used in a variety of applications.

This DSC resource can be used to address some of the most common scenarios including
the need for a Stand-Alone Certificate Authority or an Active Directory Trusted
Root Certificate Authority and the Certificate Services website for users to submit
and complete certificate requests.
In a specific example, when building out a web server workload such as an internal
website that provides confidential information to be accessed from computers that
are members of an Active Directory domain, AD CS can provide a source for the SSL
certificates that will automatically be trusted.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/)
or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any
additional questions or comments.

## Branches

### master

[![Build status](https://ci.appveyor.com/api/projects/status/2uua9s0qgmfmqqrh/branch/master?svg=true)](https://ci.appveyor.com/project/PowerShell/ActiveDirectoryCSDsc/branch/master)
[![codecov](https://codecov.io/gh/PowerShell/ActiveDirectoryCSDsc/branch/master/graph/badge.svg)](https://codecov.io/gh/PowerShell/ActiveDirectoryCSDsc/branch/master)

This is the branch containing the latest release - no contributions should be made
directly to this branch.

### dev

[![Build status](https://ci.appveyor.com/api/projects/status/2uua9s0qgmfmqqrh/branch/dev?svg=true)](https://ci.appveyor.com/project/PowerShell/ActiveDirectoryCSDsc/branch/dev)
[![codecov](https://codecov.io/gh/PowerShell/ActiveDirectoryCSDsc/branch/dev/graph/badge.svg)](https://codecov.io/gh/PowerShell/ActiveDirectoryCSDsc/branch/dev)

This is the development branch to which contributions should be proposed by contributors
as pull requests. This development branch will periodically be merged to the master
branch, and be released to [PowerShell Gallery](https://www.powershellgallery.com/).

## Contributing

Please check out common DSC Resources [contributing guidelines](https://github.com/PowerShell/DscResource.Kit/blob/master/CONTRIBUTING.md).

## Resources

- **AdcsCertificationAuthority**: This resource can be used to install the ADCS
  Certificate Authority after the feature has been installed on the server.
- **AdcsOnlineResponder**: This resource can be used to install an ADCS Online
  Responder after the feature has been installed on the server.
- **AdcsWebEnrollment**: This resource can be used to install the ADCS Web
  Enrollment service after the feature has been installed on the server.

### AdcsCertificationAuthority

This resource can be used to install the ADCS Certificate Authority after the
feature has been installed on the server.
Using this DSC Resource to configure an ADCS Certificate Authority assumes that
the `ADCS-Cert-Authority` feature has already been installed.

- **`[String]` CAType** (_Key_): Specifies the type of certification authority to
  install. { EnterpriseRootCA | EnterpriseSubordinateCA | StandaloneRootCA |
  StandaloneSubordinateCA }
- **`[PSCredential]` Credential** (_Required_): To
  install an enterprise certification authority, the computer must be joined to
  an Active Directory Domain Services domain and a user account that is a member
  of the Enterprise Admin group is required. To install a standalone certification
  authority, the computer can be in a workgroup or AD DS domain. If the computer
  is in a workgroup, a user account that is a member of Administrators is required.
  If the computer is in an AD DS domain, a user account that is a member of Domain
  Admins is required.
- **`[String]` Ensure** (_Write_): Specifies whether the Certificate Authority
  should be installed or uninstalled. { *Present* | Absent }
- **`[String]` CACommonName** (_Write_): Specifies the certification authority
  common name.
- **`[String]` CADistinguishedNameSuffix** (_Write_): Specifies the certification
  authority distinguished name suffix.
- **`[String]` CertFile** (_Write_): Specifies the file name of certification
  authority PKCS 12 formatted certificate file.
- **`[PSCredential]` CertFilePassword** (_Write_):
  Specifies the password for certification authority certificate file.
- **`[String]` CertificateID** (_Write_): Specifies the thumbprint or serial
  number of certification authority certificate.
- **`[String]` CryptoProviderName** (_Write_): The name of the cryptographic
  service provider or key storage provider that is used to generate or store the
  private key for the CA.
- **`[String]` DatabaseDirectory** (_Write_): Specifies the folder location of
  the certification authority database.
- **`[String]` HashAlgorithmName** (_Write_): Specifies the signature hash
  algorithm used by the certification authority.
- **`[Boolean]` IgnoreUnicode** (_Write_): Specifies that Unicode characters are
  allowed in certification authority name string.
- **`[String]` KeyContainerName** (_Write_): Specifies the name of an existing
  private key container.
- **`[Uint32]` KeyLength** (_Write_): Specifies the bit length for new certification
  authority key.
- **`[String]` LogDirectory** (_Write_): Specifies the folder location of the
  certification authority database log.
- **`[String]` OutputCertRequestFile** (_Write_): Specifies the folder location
  for certificate request file.
- **`[Boolean]` OverwriteExistingCAinDS** (_Write_): Specifies that the computer
  object in the Active Directory Domain Service domain should be overwritten with
  the same computer name.
- **`[Boolean]` OverwriteExistingDatabase** (_Write_): Specifies that the existing
  certification authority database should be overwritten.
- **`[Boolean]` OverwriteExistingKey** (_Write_): Overwrite existing key container
  with the same name.
- **`[String]` ParentCA** (_Write_): Specifies the configuration string of the
  parent certification authority that will certify this CA.
- **`[String]` ValidityPeriod** (_Write_): Specifies the validity period of the
  certification authority certificate in hours, days, weeks, months or years. If
  this is a subordinate CA, do not use this parameter, because the validity period
  is determined by the parent CA. { Hours | Days | Months | Years }
- **`[Uint32]` ValidityPeriodUnits** (_Write_): Validity period of the certification
  authority certificate. If this is a subordinate CA, do not specify this parameter
    because the validity period is determined by the parent CA.

#### AdcsCertificationAuthority Examples

- [Install enterprise root certificate authority](/Examples/Resources/AdcsCertificationAuthority/1-InstallCertificationAthority.ps1)
- [Retire certificate authority](/Examples/Resources/AdcsCertificationAuthority/2-RetireCertificationAthority.ps1)

### AdcsOnlineResponder

This resource can be used to install an ADCS Online Responder after the feature
has been installed on the server.
Using this DSC Resource to configure an ADCS Certificate Authority assumes that
the ```ADCS-Online-Responder``` feature has already been installed.
For more information on ADCS Online Responders, see [this article on TechNet](https://technet.microsoft.com/en-us/library/cc725958.aspx).

- **`[String]` IsSingleInstance** (_Key_): Specifies the resource is a single
  instance, the value must be 'Yes' { Yes }
- **`[String]` CAConfig** (_Write_): CAConfig parameter string. Do not specify
  this if there is a local CA installed.
- **`[PSCredential]` Credential** (_Required_): If
  the Online Responder service is configured to use Standalone certification
  authority, then an account that is a member of the local Administrators on the
  CA is required. If the Online Responder service is configured to use an Enterprise
  CA, then an account that is a member of Domain Admins is required.
- **`[String]` Ensure** (_Write_): Specifies whether the Online Responder feature
  should be installed or uninstalled. { *Present* | Absent }

#### AdcsOnlineResponder Examples

- [Install Online Certificate Status Protocol (OCSP) server](/Examples/Resources/AdcsWebEnrollment/1-InstallOnlineResponder.ps1)

### AdcsWebEnrollment

This resource can be used to install the ADCS Web Enrollment service after the
feature has been installed on the server.
Using this DSC Resource to configure an ADCS Certificate Authority assumes that
the ```ADCS-Web-Enrollment``` feature has already been installed.
For more information on Web Enrollment services, see [this article on TechNet](https://technet.microsoft.com/en-us/library/cc732517.aspx).

- **`[String]` IsSingleInstance** (_Key_): Specifies the resource is a single
  instance, the value must be 'Yes' { Yes }
- **`[String]` CAConfig** (_Write_): CAConfig parameter string. Do not specify
  this if there is a local CA installed.
- **`[PSCredential]` Credential** (_Required_): If
  the Web Enrollment service is configured to use Standalone certification authority,
  then an account that is a member of the local Administrators on the CA is required.
  If the Web Enrollment service is configured to use an Enterprise CA, then an
  account that is a member of Domain Admins is required.
- **`[String]` Ensure** (_Write_): Specifies whether the Web Enrollment feature
  should be installed or uninstalled. { *Present* | Absent }

#### AdcsWebEnrollment Examples

- [Install web enrollment server](/Examples/Resources/AdcsWebEnrollment/1-InstallWebEnrollment.ps1)

## Versions

### Unreleased

- BREAKING CHANGE: Renamed module to ActiveDirectoryCSDsc - see
  [issue #38](https://github.com/PowerShell/xAdcsDeployment/issues/38)
- Enabled PSSA rule violations to fail build - Fixes [Issue #44](https://github.com/PowerShell/ActiveDirectoryCSDsc/issues/44).

### 1.4.0.0

- xAdcsCertificateAuthority: CertFilePassword invalid type - fixes
  [issue #36](https://github.com/PowerShell/xAdcsDeployment/issues/36)

### 1.3.0.0

- Updated to meet HQRM guidelines - fixes
  [issue #33](https://github.com/PowerShell/xAdcsDeployment/issues/33).
- Fixed markdown rule violations in README.MD.
- Change examples to meet HQRM standards and optin to Example validation
  tests.
- Replaced examples in README.MD to links to Example files.
- Added the VS Code PowerShell extension formatting settings that cause PowerShell
  files to be formatted as per the DSC Resource kit style guidelines.
- Opted into Common Tests 'Validate Module Files' and 'Validate Script Files'.
- Corrected description in manifest.
- Added .github support files:
  - CONTRIBUTING.md
  - ISSUE_TEMPLATE.md
  - PULL_REQUEST_TEMPLATE.md
- Resolved all PSScriptAnalyzer warnings and style guide warnings.
- Converted all tests to meet Pester V4 guidelines - fixes
  [issue #32](https://github.com/PowerShell/xAdcsDeployment/issues/32).
- Fixed spelling mistakes in README.MD.
- Fix to ensure exception thrown if failed to install or uninstall service - fixes
  [issue #3](https://github.com/PowerShell/xAdcsDeployment/issues/3).
- Converted AppVeyor.yml to use shared AppVeyor module in DSCResource.Tests - fixes
  [issue #29](https://github.com/PowerShell/xAdcsDeployment/issues/29).

### 1.2.0.0

- xAdcsWebEnrollment:
  - xAdcsWebEnrollment.psm1 - Change reference and variable from CAType to CAConfig

### 1.1.0.0

- Converted AppVeyor.yml to pull Pester from PSGallery instead of Chocolatey.
- Changed AppVeyor.yml to use default image.
- xAdcsCertificateAuthority:
  - Change property format in Readme.md to be standard layout.
  - Converted style to meet HQRM guidelines.
  - Added verbose logging support.
  - Added string localization.
  - Fixed Get-TargetResource by removing IsCA and changing Ensure to return whether
    or not CA is installed.
  - Added unit tests.
  - Updated parameter format to meet HQRM guidelines.
- xAdcsOnlineResponder:
  - Change property format in Readme.md to be standard layout.
  - Added unit test header to be latest version.
  - Added function help.
  - Updated parameter format to meet HQRM guidelines.
  - Updated resource to meet HQRM guidelines.
- xAdcsWebEnrollment:
  - Change property format in Readme.md to be standard layout.
  - Added unit test header to be latest version.
  - Added function help.
  - Updated parameter format to meet HQRM guidelines.
  - Updated resource to meet HQRM guidelines.
- Added CommonResourceHelper.psm1 (copied from xPSDesiredStateConfiguration).
- Removed Technet Documentation HTML file from root folder.
- Removed redundant code from AppVeyor.yml.
- Fix markdown violations in Readme.md.
- Updated readme.md to match DSCResource.Template\Readme.md.

### 1.0.0.0

- Moved Examples folder into root.
- Removed legacy xCertificateServices folder.
- Prevented Unit tests from Violating PSSA rules.
- MSFT_xAdcsWebEnrollment: Created unit tests based on v1.0 Test Template.
                           Update to meet Style Guidelines and ensure consistency.
                           Updated to IsSingleInstance model. **Breaking change**
- MSFT_xAdcsOnlineResponder: Update Unit tests to use v1.0 Test Template.
                             Unit tests can be run without AD CS installed.
                             Update to meet Style Guidelines and ensure consistency.
- Usage of WinRm.exe replaced in Config-SetupActiveDirectory.ps1 example file
  with Set-WSManQuickConfig cmdlet.

### 0.2.0.0

- Added the following resources:
  - MSFT_xADCSOnlineResponder resource to install the Online Responder service.
- Correction to xAdcsCertificationAuthority property title in Readme.md.
- Addition of .gitignore to ensure DSCResource.Tests folder is committed.
- Updated AppVeyor.yml to use WMF 5 build environment.

### 0.1.0.0

- Initial release with the following resources
  - xAdcsCertificationAuthority and xAdcsWebEnrollment.
