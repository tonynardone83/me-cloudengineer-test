<p>Question 5 : A CMK key I have created and used to encrypt contents of my S3 bucket is deleted by mistake, how do I recover the contents or key ?</p>
<p>&nbsp;</p>
<p>Answer:</p>
<p>If the CMK has been deleted, I would proceed in re-applying the CMK&rsquo;s Keys Material and Import Token based off a backup, this will re-enable the Key and make it available for re-use,&nbsp;particularly against the S3 bucket that has been assigned the CMK for data encryption.</p>
<p>Alternatively, if the key has been scheduled for deletion, then the deletion can be revoked, provided the revoke action has occurred prior to the Keys scheduled deletion.</p>
