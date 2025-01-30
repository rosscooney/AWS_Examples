# AWS Examples

Many AWS users over-engineer their infrastructure, either by over-scaling for hypothetical future needs or by using too many AWS services just because they can. 

Iam a firm believer that infrastructure needs to be simple, secure and as cheap as possible. This repo contains some ideas on how to achieve this...and some non-negociable principles.

Notes: 
1. This repo is designed for a PHP / Nginx / mysql stack...however the principles will extend to other stacks.
2. You need to understand the recommendations, look at the suggested archiceture design and then make edits to suit your applicaiton.


## Non-negociable principles.

Regardless of the size of your architecture, you should follow these principles: 

### Make it tidy
1. Your AWS account is setup using AWS Orgs, and access is granted using the IAM Identity Centre.
2. EC2 instances are disposable. There shiuld be no assets on the EC2 images and all software is built/compiled/installed by the CI/CD system
3. All infrastructure is built using CloudFormation and built 'on the fly' from hardened AMI's

### Store everything where it belongs
1. Assets belong in S3
2. Data belongs in a database (RDS Aurora preferrably)
3. Sessions belong in Elasticache (Redis, or Valkey in the future)
4. Infrastructure belongs in code (CloudFormation)
5. Application config files belong on a shared storage device (FSx)

The minimum stack comprises of these elements:

![AWS Icons](images/AWS_Icons_1.png)


## Rightsizing your stack

The key to building the right AWS infrastructure is striking a balance between technical excellence and financial practicality. Don’t over-engineer your stack. Keep it simple, scalable, and cost-effective.

Let’s start by talking about some of the most common mistakes we see when building AWS infrastructure. One of the biggest pitfalls is over-scaling. It’s easy to think, “What if our user base grows by 10x next year? Let’s architect for that now.” While it’s great to be forward thinking, over building infrastructure for future growth can quickly lead to unnecessary costs and complexity.

Another problem I see a lot of is what I like to call the spaghetti soup of AWS services. If you arent careful the system can become a tangled web of services that no one can keep track of. While AWS offers all these great options, throwing every service you can think of into your architecture often makes things harder to manage. You end up paying for services you don’t need, and more importantly, it makes it harder to explain your choices to someone outside your team.

These kinds of over engineered stacks are often not only costly but also hard to scale and maintain. And when we’re talking about convincing the CFO to approve your infrastructure budget, they’re looking for efficiency, clarity, and a clear ROI—not a soup of services they don’t understand.

**1.	Early Stage (Proof of Concept / MVP):**
- In the early stages of a project, the focus should be on rapid development, simplicity, and low costs. You want to get your product into the hands of users quickly and iterate based on feedback. In this phase, over-architecture is your enemy. You don’t need auto-scaling groups or multi-AZ deployments yet. The goal here is to build just enough infrastructure to support a small user base, and spend as little as possible while you’re validating the product.


2. **Growth Phase (Scaling Features / Expanding User Base):**

- Once your MVP is successful and you start seeing traction, it’s time to scale your infrastructure to handle increased traffic. In this phase, you need to begin planning for growth, but don’t go overboard. Services like Load Balancers, Auto Scaling and CloudFront can help handle traffic surges. However, don’t rush into complex architectures. Stick to services that will allow you to scale quickly without adding too much overhead. Also, be mindful of your costs at this stage—AWS can get expensive fast, so it’s critical to right-size your infrastructure for the traffic you’re seeing, rather than over-provisioning for growth that hasn’t materialised yet.

3. **Mature Stage (High Traffic / Optimization):**
- At this stage, your product is stable and your infrastructure needs to be optimised for both performance and cost. You’ll want to focus on cost efficiency, using AWS’s savings plans or reserved instances to lower your costs while maintaining performance.  At this stage, the architecture complexity will be higher, but it should still be manageable and cost-effective.  You’ll likely be looking at multi-region, multi-availability zone setups. Focus on refining your monitoring and logging capabilities (with services like CloudWatch and X-Ray) to ensure you’re catching bottlenecks or inefficiencies before they become a problem.




