# AWS-ARC
Architecting on AWS
## IAM Role 실습
1. Google OTP를 다운받아 AWS 계정 루트 사용자의 보안 설정을 업데이트 합니다.
2. test-user 사용자를 생성한다. (Console, AWS CLI에 접근 가능한 유형)
3. Test-groups 이름으로 그룹을 생성한다.
   해당 그룹에 test-user를 포함시킨다.
4. Test-groups 그룹에 EC2-Full Access 정책을 찾아서 할당한다.

[IAM 실습 2 ]
1. IAM 사용자를 생성한다 (권한을 EC2FullAccess 할당한다.)
2. IAM 사용자로 로그인해서 EC2에 대한 권한과 다른(S3)에 대한 권한 없을을 확인한다.
3. AWS 계정 루트로 로그인 한다.
4. IAM 사용자에게 인라인 정책으로 다음 AssumRole 정책을 할당한다.

```JSON

{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "sts:AssumeRole",
    "Resource": "arn:aws:iam::507815402614:role/s3*"
  }
}

```


5. 역할(Role)을 생성한다. (S3FullAccess 권한 할당)
   역할만들기 --> 다른AWS계정 선택 --> 계정ID 입력 --> 정책필터에 s3 입력해서 AmazonS3FullAccess 정책 선택
   다음클릭 --> 태그추가(키:Name , 값 : S3 Full Access Role)입력
6. IAM 사용자가 할당받을 정책을 생성한다. (기존 정책을 이용해도 된다. 정책이름 체크필수)
    ** s3FullAccess 권한 할당 정책을 생성한다. (이름 : s3FullAccessPolicy)
7. IAM 사용자로 로그인해서 계정정보를 클릭하고 "역할전환"을 선택한다.
    다음을 입력하고 "역할 전환"버튼을 클릭한다.
    계정* : 507815402614     <-- 역할을 할당한 계정 ID
    역할* : s3FullAccess     <-- 전환할 정책 이름  s3-Full-Access-Role
8. 변경된 역할정보를 계정정보(우측상위)에서 확인시켜주고 정책에 맞는 권한으로 전환된것을 확인한다.
9. 오른쪽 위에 "역할전환내역 이름"을 클릭하고 iamuser2(으)로 돌아가기를 클릭한다.
10. 원래 권한으로 복귀한 것을 확인한다.
