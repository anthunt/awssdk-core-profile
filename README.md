# awssdk-core-profile
aws java sdk plugin for merged profile with config file
>Extension Project for Java AWS sdk.
The ProfileCredentialsProvider Class provided by the AWS JAVA SDK recognizes only the ~/.aws/credentials setting to provide Credentials.
This project will help you set up the merged Profile Credentials by importing all of the settings from the ~/.aws/credentials and ~/.aws/config files.

# ~/.aws/credentials
    [default]
    aws_access_key_id = Your Accesskey
    aws_secret_access_key = Your SecretKey

# ~/.aws/config
    [default]
    region = ap-northeast-2
    output = json

    [profile sample]
    role_arn = arn:aws:iam::000000000000:role/SampleRole
    source_profile = default
    region = us-east-1

# Example - Test.java
    import com.amazonaws.services.s3.AmazonS3;
    import com.amazonaws.services.s3.AmazonS3ClientBuilder;
    import com.anthunt.aws.sdk.profile.MergedProfileCredentialsProvider;
    
    public class Test {
        public static void main(String[] args) {
            AmazonS3 amazonS3 = AmazonS3ClientBuilder
                                .standard()
                                .withCredentials(new MergedProfileCredentialsProvider("sample"))
                                .build();
        }
    }
