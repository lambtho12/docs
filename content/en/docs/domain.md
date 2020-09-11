---
title: Get Your Own Domain Name
date: 2017-12-24
type: book
weight: 100
---

If you choose a deployment option such as Netlify or Github pages, you will be automatically assigned a free URL for your website. You can further personalize your website with your own domain name.

We can highly recommend [Namecheap](https://affiliate.namecheap.com/?affId=105828) for **registering a domain**, as they provide great value for money whilst providing fast support. To find a good domain that is available, try a mix of your first and last names or initials, with either a `.com` or `.me` ending.

**For Netlify deployments**, once your domain is registered, navigate to the *Custom domains* section of the Netlify admin panel and then follow [their wizard](https://www.netlify.com/docs/custom-domains/#assigning-a-custom-domain) to assign your domain to your site.

**For Github deployments**, you'll need to login to your domain registrar to point your domain to Github, and create a `CNAME` file in the `static` folder of your website, so that Github knows your intentions. For more information, check out the [domains guide by Github](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/).

**For Gitlab deployments**, you'll need to login to your domain registrar to point your domain to Gitlab, and verify that you indeed own this domain using a TXT record. For more information, check out the [domains guide by Gitlab](https://docs.gitlab.com/ee/user/project/pages/custom_domains_ssl_tls_certification/).

Remember that after you have setup a custom domain, you will need to wait approximately 24-48 hours for the DNS to propagate and then you'll need to update `baseurl` in your `config.toml` to your new URL, regenerate your site (refer to the previous section), and redeploy.
