# Use the official .NET 5.0 Lambda runtime image
FROM public.ecr.aws/lambda/dotnet:7

# Copy all the contents from the publish directory to the Lambda task root
COPY ./publish/ ${LAMBDA_TASK_ROOT}

# Set the Lambda entry point (adjust to your Lambda function's namespace and method)
CMD [ "AWSLambdaForTestingProject::AWSLambdaForTestingProject.Function::FunctionHandler" ]