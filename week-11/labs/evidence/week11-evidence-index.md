# Week 11 evidence index

Simulator captures from attempt F6FAF6. Hash detects content changes; it is not proof of live AD administration.

## EV-F6FAF6-001

- Slot E01 · M01 · revision 5
- Directory trace: Alex person, both accounts, OU, one AD grant path, one cloud role path
- SHA-256 e33482d234cfe1aed7a49a2d77c1d3f8ae70b72e9c5adec257b2e0e724a56662
- Caption: The selected records show that Alex Morgan has two enabled accounts (Active Directory & Cloud Identity).

## EV-F6FAF6-002

- Slot E02 · M01 · revision 5
- Comparison of Blair, Finley and Drew
- SHA-256 559744caa77cb40f3550e02dfa6017fe2731df38075bba80a39104ab35eb3473
- Caption: Blair Chen and Finley Ross accounts are enabled in Cloud Identity. Drew Patel's accounts are disabled in Active Directory and Cloud Identity. This associated evidence only tells if the accounts are enabled or disabled but, does not give details about the respective person's groups and effective access, other accounts, associated resources, etc. This additional evidence is located in the users' account details.

## EV-F6FAF6-003

- Slot E03 · M02 · revision 7
- Successful sign-in + the access result before your change
- SHA-256 f2dda06798c1fe380d190a7b1fda74df04bb0618b62b4e7c63a94ec98e48eee3
- Caption: The sign-in record proves that Blair's account authenticated successfully (there are no errors specifically regarding logging in).  The evidence also shows that Blair's account was denied access to read the resource, Case Summaries (the before-change access test record).

## EV-F6FAF6-004

- Slot E04 · M02 · revision 20
- Membership/access change audit + read result + update result
- SHA-256 a400b9d93dbf8b19418049cfc02ccf616acb5f3230a18efd24d80f855a91c115
- Caption: Blair's account status was changed to read access but, access for Blair to update the resource is still denied.

## EV-F6FAF6-005

- Slot E13 · M05 · revision 26
- Alex before/after access and changes
- SHA-256 01187d5249f415033d5abe337d38254014e6d9ccaeb595e40d8a374afc8161d5
- Caption: Alex is allowed Response Queue / read and denied Audit Evidence / export.

## EV-F6FAF6-006

- Slot E13 · M05 · revision 26
- Alex before/after access and changes
- SHA-256 562a0f8fe0e1f85aae68fb0d1d9713df3712c28073fddf07d19f351c062d3cb2
- Caption: I retested Alex's cloud account. Response Queue / read is allowed and Audit Evidence / export is denied.

## EV-F6FAF6-007

- Slot E14 · M05 · revision 34
- Finley session/status/revocation evidence
- SHA-256 0ed066610736788f278abaf8cc742373317b092619f4b70f64a49626d23488fe
- Caption: Check Finley can no longer sign in. The evidence shows "Sign-in failed: the account is disabled".

## EV-F6FAF6-008

- Slot E17 · M06 · revision 34
- Two distinct findings with raw-event references and correlation
- SHA-256 5ea83e58f9c8fd4e257381300aa2de2cfda287cc316dfdb21dc34233b20811dc
- Caption: The selected record support my observation that Drew's account is disabled.

## EV-F6FAF6-009

- Slot E17 · M06 · revision 34
- Two distinct findings with raw-event references and correlation
- SHA-256 5ea83e58f9c8fd4e257381300aa2de2cfda287cc316dfdb21dc34233b20811dc
- Caption: The selected record support my observation that Drew's account is disabled.

## EV-F6FAF6-010

- Slot E18 · M06 · revision 34
- Benign/ambiguous comparison
- SHA-256 65527810d2d1b7c1feb1f0ade65eebe54415c0b848504ddbccf03d83d1766365
- Caption: Drew's account is disabled.

## EV-F6FAF6-011

- Slot E17 · M06 · revision 34
- Two distinct findings with raw-event references and correlation
- SHA-256 3e93353b994ea4ec586288071eb7f52a13f0fafc909693bd6540c78afae540ac
- Caption: The selected records show when Blair's password authentication failed and when it was successful. These records support my observation that the incorrect password was entered the first time. The evidence does not determine what the passwords are.

## EV-F6FAF6-012

- Slot E18 · M06 · revision 34
- Benign/ambiguous comparison
- SHA-256 46688bf74c841aa2292adaa3b17eb57e746ce9d0c20c1286c748ade1bb91054d
- Caption: The selected records show the account holder was removed from the group, the account was disabled, and access was revoked.

## EV-F6FAF6-013

- Slot E19 · M06 · revision 34
- Completed case file / versioned export
- SHA-256 85bb586c1effd10ae5bebe4941aa8025d924fdb21c53fa7ce5e9731daa283bba
- Caption: The Case File references these records to support that Drew's account was disabled and there was an unsuccessful authentication on Blair's account followed by a successful authentication (as well as other action on Blair's account).
