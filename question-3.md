<p>Question 3:&nbsp; Design an enterprise IAM solution to provide access to users, Applications, and services across the organization while ensuring controls are in place to ensure restrictions can be implemented on a least privileged requirement.</p>
<p>Answer:</p>
<p>I would consider a product like Okta as the IAM solution as this provides easy enablement of single sign-on and security to cloud platforms.</p>
<p>Since Okta easily integrated with cloud platform as an Identity Provider, it can be leveraged to facilitate access control to cloud platforms via group assignment in a few simple steps:</p>
<ul>
<li>Create SSO Integration with Cloud Platform e.g. Salesforce</li>
<li>Create your users in Salesforce</li>
<li>Create a group in Okta and assign the newly created group to the Salesforce SSO application configuration</li>
<li>Assign permitted users to the group (users are generally imported into the Okta platform via an Active Directory sync)</li>
</ul>
<p>Users will then only be permitted to sign into the application provided they have been added to the applications group application assignment, in most cases an account must be created within the service providers platform in order for the SAML assertion to complete successfully.</p>
<p>Furthermore, to enforce least privilege, this is sometimes done at the Service Provider end, administrators responsible for the identities must ensure they provide sufficiently level of permission to the user prior to configuring its group assignment in Okta.</p>
<p><strong>Enterprise IAM Solution:</strong></p>
<p>As far as an enterprise IAM solution I would go with something that looks like the below diagram, as Okta can extend out and integrate with many cloud platforms for authentication:</p>
<p>&nbsp;<img src="https://github.com/tonynardone83/me-cloudengineer-test/blob/master/images/iam-okta.png" alt="" /></p>
