# aws-mfa
## Script work-around for mfa-required assumption of roles

This is designed to be used when you enforce MFA on all users, including their use of the AWS API.

To enforce mfa, please see the following modules:
- https://github.com/QuiNovas/terraform-modules/tree/master/aws/user
- https://github.com/QuiNovas/terraform-modules/tree/master/aws/user-role
- https://github.com/QuiNovas/terraform-modules/tree/master/aws/assume-role-group

Once you have MFA enforcement setup and cross-account roles established, you use this script in place of the normal `aws` command.

Recommendations:
- Place `aws-mfa` in your path, and make it executable. `/usr/local/bin` is my preferred location.
- For each user profile in `~.aws/credentials` that you wish to switch roles for, create a file in `~/.aws/` by that name. For instance, profile `foo` and file `~/.aws/foo`
- Then create a symbolic link from your new file to `default`. This allows you to use one default profile for everything.
- Within your new file, place the following two lines:

1. `export AWS_MFA_ROLE_ARN=<the arn to the role that you want to assume/switch to>`
2. `export AWS_MFA_ARN=<the arn of YOUR mfa device>`

Running `aws-mfa` - when you run this, it will ask you first for your profile (I use `default`) and then the MFA token of your specified profile user.

Enjoy!

## destroy-default-vpcs

This is designed to delete all default VPCs and associated gateways and subnets for an AWS account.  This script relies on the same variables as the aws-mfa script.

WARNING: This script is desctructive and has not been widely tested.  Use it at your own risk!
