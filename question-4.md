<p>Question 4: I have deployed a service in VPC B and am invoking an API call to the service from an instance inside VPC A. The API call fails. How do I troubleshoot?</p>
<p>&nbsp;</p>
<p>Answer:</p>
<p>I would start off by checking network connectivity:</p>
<p>Step 1: Send a ping or traceroute from VPC B from VPC A</p>
<ul>
<li>Ping &ndash; Is there a response</li>
<li>Traceroute &ndash; Any timeout&rsquo;s in the path between VPC B to VPC A</li>
</ul>
<p>Step 2:&nbsp;Check VPC B service, determine if it is Online, if it is an EC2 instance Power it back on</p>
<p>Step&nbsp;3: If we were to assume the two VPC&rsquo;s are peered then I would ensure a peering between VPC&rsquo;s exist, if they have not been peered then they must be peered and approved</p>
<p>Step&nbsp;4: Ensure that the VPC&rsquo;s have route tables associated to the subnets</p>
<ul>
<li>One route table for the subnet serving the API &ndash; ensure this subnet can route from VPC A to VPC B through peering</li>
<li>One route table for the subnet serving the instance invoking the API - ensure this subnet can route from VPC B to VPC A through peering</li>
</ul>
<p>Step 2:&nbsp;Check&nbsp;the route tables within each VPC, ensuring that all routing to and from VPC&rsquo;s traverses through the peering connections</p>
<p>Step 5: Check the security groups assigned to the service in VPC B ensuring incoming traffic from the instance inside VPC A is permitted</p>
<p>Step 6: Check to see if there are any expired API keys that were issued by service in VPC B</p>
<p>Step 7: Determine if any Firewalls (iptables) within service in VPC B are blocking incoming traffic from VPC A</p>
<p>&nbsp;</p>
