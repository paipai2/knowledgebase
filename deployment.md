# Deployment SOP

1. Is $variable in your script contains test value?

2. Is your new deployment thing tested by client?

3. Have you decided to temporarily close down withdrawal or transfer or any other spending action to prevent user spend illegal money from program bugs?

4. Will your new deployment just open to certain users to avoid error happen to large scale of users?

5. For critical business conditions in your coding, have you added email to notify you for further monitor?

6. Have you setup check script to ensure work is fine? It is advisable that run check script more frequent if you new deployment is critical.

7. For any spending action. Please ensure that
    - Transfer page has preview and confirmation.
    - TAC or OTP is required.
    - Secondary password/security password/PIN is required if applicable.
    - Add minimum spend (to prevent end user fill in -ve amount)
    - Duplicate insert prevention.
    
8. Remember to keep monitor from time to time. This includes
    - Correctness of DB data.
    - Accurancy of monetary payout.
    - Check script has no bug and done its work.
    - No duplicate insert.
    - Activity log properly.
    
9. Check are there any echo, debug, print_r, var_dump in your script to prevent leaking of sensitive debug info.

