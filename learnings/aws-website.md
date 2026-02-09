## Services
<b>S3</b> &rarr; store website files

<b>CloudFront</b> &rarr; Content Delivery Network (CDN)

<b>ACM</b> &rarr; SSL certificate

<b>Route 53</b> &rarr; custom domain routing

<b>WAF</b> &rarr; protection against vulnerabilities (OWASP)

<p align="center">
    <img src="../assets/aws-website.png" alt="AWS Website">
</p>

1. Setup S3
   - bucket name as website name with correct sub-domain (hussainkazarani.com)
   - private bucket 

2. ACM and Route 53
   - set up Custom DNS in namecheap and add in Hosted Zone
   - ACM is in North Virginia
   - create for `wwww.hussainkazarani.com` and `hussainkazarani.com`

3. Setup CloudFront
   - use OAC
   - distribution name should be you domain
   - refirect HTTP to HTTPS
   - edit distribution and copy thr policy and paste in S3 bucket policy <b>(S3 &rarr; Permissions &rarr; Policy)</b>

4. Configure Route 53
   - add both the domain in certificate as `A-Type Alias` record 
   - route traffic through `CloudFront Distribution`
   - redirect `www` domain to main domain
   - above can be done using `CloudFront Function` <b>(CloudFront &rarr; Behaviour &rarr; Edit Default &rarr; Function Associations &rarr; Viewer Requests &rarr; Add the created function)</b>