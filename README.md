# functions
#!/bin/bash
# Environment variables
ENVIRONMENT=$1

check_num_of_args() 
{"\n# Checking the number of arguments\nif [ \"$#\" -ne 0 ]; 
then\n    echo \"Usage: $0 <environment>\"\n    exit 1\nfi\n"}

activate_infra_environment() {
"\n# Acting based on the argument value\nif [ \"$ENVIRONMENT\" == \"local\" ]; 
then\n  echo \"Running script for Local Environment...\
"\nelif [ \"$ENVIRONMENT\" == \"testing\" ]; 
then\n  echo \"Running script for Testing Environment...\"
\nelif [ \"$ENVIRONMENT\" == \"production\" ];
then\n  echo \"Running script for Production Environment...\
"\nelse\n  echo \"Invalid environment specified. Please use 'local', 'testing', or 'production'.\"\n  exit 2\nfi\n"
}

# Function to check if AWS CLI is installed
check_aws_cli() {
"\n    if ! command -v aws &> /dev/null; then\n    
echo \"AWS CLI is not installed. Please install it before proceeding.\"\n    
return 1\n    fi\n"
}

# Function to check if AWS profile is set
check_aws_profile() {
"\n    if [ -z \"$AWS_PROFILE\" ]; then\n   
 echo \"AWS profile environment variable is not set.\"\n      
 return 1\n    fi\n"
 }

check_num_of_args
activate_infra_environment
check_aws_cli
check_aws_profile


#credentials files
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY

[profile testing]
aws_access_key_id = YOUR_TESTING_ENVIRONMENT_ACCESS_KEY_ID
aws_secret_access_key = YOUR_TESTING_ENVIRONMENT_SECRET_ACCESS_KEY

[profile production]
aws_access_key_id = YOUR_PRODUCTION_ENVIRONMENT_ACCESS_KEY_ID
aws_secret_access_key = YOUR_PRODUCTION_ENVIRONMENT_SECRET_ACCESS_KEY

# config file (~/.aws/config)
[default]
region = us-east-1
output = json

[profile testing]
region = us-west-2
output = json

[profile production]
region = us-west-2
output = json




