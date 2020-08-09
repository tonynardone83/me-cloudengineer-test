<p>Question 1:&nbsp;</p>
<p>Design a golden master AMI build workflow identifying the key stages and suggest technologies which might be used to implement.&nbsp; Use of AWS native services is preferred.</p>
<p>Answer:</p>
<p><strong><u>Identify Key Stages to build Golden Master AMI: </u></strong></p>
<p><strong>Step 1 - Requirement gathering</strong></p>
<ul>
<li>Operating system Requirement &ndash; (Linux or Windows or other)</li>
</ul>
<ul>
<li>Baseline Software Requirements &ndash; (Gather understanding of Software to be installed on the Golden Image, e.g. GIT, Python or other)</li>
<li>Compute power Requirement (e.g. EC2 instance type, although not essential as image can be scaled up or down at any stage)</li>
<li>Security Hardening Requirements (Agent&rsquo;s, Security Patches, OS Patches)</li>
</ul>
<p><strong>Step 2 - Validate AMI</strong></p>
<ul>
<li>Test and deployment</li>
<li>Validate Golden AMI with Security team to ensure patching is at required level and meets their satisfaction,</li>
<li>Gain IT approval before proceeding with deployment</li>
</ul>
<p><strong>Step 3 - Deploy</strong></p>
<ul>
<li>Deploy AMI</li>
<li>Provide required users with IP and credentials (Windows), or IP, Access Key and Secret (Linux)</li>
<li>If requirements change create new version of Pipeline and re-deploy (see below as this relates to the suggested technology)</li>
</ul>
<p><strong><u>Suggested Technologies</u></strong></p>
<ul>
<li><u>AWS Image Builder (<strong>best option)</strong></u></li>
<li>EC2 Management Console (Can be used, an easy option to Create AMI directly from portal)</li>
<li>Cloudformation</li>
<li>AWS CLI&nbsp;</li>
</ul>
<p>I find this as the best option, image builder will provide an easy way to build a Golden AMI image in a Pipeline fashion, this is good for repeatability and continuous improvement.</p>
<p>Image builder allows to create AMI&rsquo;s with essential components via the AWS Console GUI in 3 steps:</p>
<ul>
<li>Define <strong>Component</strong> &ndash;</li>
</ul>
<p>Define software, scripts and OS tweaks that will need to run as part of the build, all defined in YAML document.</p>
<ul>
<li>Define <strong>Recipe</strong> &ndash;</li>
</ul>
<p>Define the Golden Image OS, Compute, VPC, Subnets, Security Groups, while also attaching the Component created&nbsp;</p>
<ul>
<li><strong>Build Pipeline</strong> &ndash;</li>
</ul>
<p>Build a pipeline out of the Recipe and Run. This builds a Golden AMI and will be available in AMI within the EC2 Management Console</p>
<p><strong>Key Stage 4:</strong> <strong>Locate Golden Image AMI </strong></p>
<p>Once the Pipeline is complete, we should have access to our AMI from the EC2 Management console.</p>
<p><strong>Workflow Diagram:</strong></p>
<p><strong><img src="https://github.com/tonynardone83/me-cloudengineer-test/blob/master/images/workflow-diagram.png" alt="" /></strong></p>
