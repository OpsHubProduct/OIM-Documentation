If you have forgotten your password, <code class="expression">space.vars.SITENAME</code> provides a secure way to reset it.

- On the Login page, click the **Forgot Password** link in the login form, as shown below.

<p align="center">
  <img src="../assets/Getting_Started_With_Application_Image_1G_a.png" width="680"/>
</p>

- You will be redirected to the Forgot Password page. Enter your **username** associated with your account and click on **Reset Password** to proceed.

<p align="center">
  <img src="../assets/ForgotPassword.png" width="680"/>
</p>


Upon clicking **Reset Password**, a reset link will be sent to the registered email address associated with the provided username.

- If OpsHub system is configured with SMTP system, the email is sent using the **Sender Email-id** configured in the SMTP system.
- If OpsHub system is not configured with SMTP system or the configuration is invalid, the email is sent using the default <code class="expression">space.vars.SITENAME</code> user.

<p align="center">
  <img src="../assets/ResetLinkMessage.png" width="680"/>
</p>

<p align="center">
  <img src="../assets/forgot_password_email.png" width="680"/>
</p>

- Open your registered email inbox, locate the password reset email, and click on the **Reset Password** link provided. This will redirect you to the Reset Password page.

<p align="center">
  <img src="../assets/ResetPassword.png" width="680"/>
</p>

- Enter a new password, confirm it and click on **Change Password** to save your new password. Ensure that it adheres to the default password policy configured in the system. To know more, refer to [Default Password Policy](../manage/administrator/login-server-management.md#password-policy-configuration).  

- Once the password is successfully reset, you will be redirected back to the Login page, where you can log in using your updated credentials.

<p align="center">
  <img src="../assets/LoginAfterReset.png" width="680"/>
</p>

---

After successfully logging in, you can continue using <code class="expression">space.vars.SITENAME</code> for integration configuration. Refer to [Overview of Integration](../integrate/overview-of-integration.md) to get started.
