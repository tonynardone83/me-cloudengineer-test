<p>Question 2: Currently connectivity between AWS accounts and on-premise networks are provided via peering and site-to-site vpn&rsquo;s.&nbsp; Design a network topology that will allow scalable connectivity both across accounts and to on premise networks, and discuss:</p>
<p>- Network migration strategies.</p>
<p>- Security considerations and provisions.</p>
<p>&nbsp;</p>
<p>Answer (Keeping this high level as much as possible):</p>
<p>I would consider building a Transit Gateway in a separate AWS Account, this will facilitate the traffic between accounts and on-premise for all attached VPC&rsquo;s, it will also provide a more scalable solution to peering, additionally there is a reduction to the configuration required on the on-premise VPN Firewall.</p>
<p>&nbsp;</p>
<p><strong>High Level Design (based off my approach):</strong></p>
<p><strong><img src="https://github.com/tonynardone83/me-cloudengineer-test/blob/master/images/transit-gateway.png" alt="" /><img src="https://github.com/tonynardone83/me-cloudengineer-test/blob/master/images/transit-gateway.png" alt="" /></strong></p>
<p><strong>Implementation Explained:</strong></p>
<ul>
<li>Attach VPC B and VPC C to the Transit Gateway in Account A</li>
<li>Create new Site-to-Site VPN connection for Transit Gateway to On-Prem, this is used for Account A&rsquo;s on-premise connectivity</li>
<li>Update Routing on VPC B and VPC C, ensuring traffic destined to On-Premise must traverse through the Transit Gateway, this also includes all communication between VPC B and VPC C (as this appears to be an existing requirement in the question)</li>
</ul>
<p><strong>Migration Strategy (Following the design diagram):</strong></p>
<ul>
<li>Build New AWS Account for the Transit Gateway</li>
<li>Create new Site-to-Site VPN connection for connectivity between Transit Gateway to On-Premise</li>
<li>Configure Transit Gateway VPC and VPN Associations</li>
<li>Configure Transit Gateway, routing and route propagation</li>
<li>Update Route tables attached to VPC B (Account B) and VPC C (Account C) ensuring traffic between them traverses through Transit Gateway Target</li>
<li>Update Routing on VPC B (Account B) and VPC C (Account C) ensuring traffic destined On-Premise transverses through Transit Gateway Target</li>
<li>Existing peering&rsquo;s from VPC B to VPC C can be removed as they are no longer required</li>
<li>Decommission VPN tunnels for Account B and Account C as they are no longer required</li>
</ul>
<p><strong>Security Considerations:</strong></p>
<ul>
<li>Account A is only required for Network Engineering Team only this should be controlled via AWS IAM and not to be access by other teams</li>
<li>Default route table association and propagation can be disabled if communication between VPC&rsquo;s (in Account B and Account C) is not required or if network segregation is preferred, this should be done when creating the Transit Gateway in Account A</li>
</ul>
<p><strong>Why Transit Gateways:</strong></p>
<p>This will allow for scale, subsequent Account VPC will only need to attach to the Transit Gateway in Account A simplifying connectivity with a centrally managed gateway.</p>
