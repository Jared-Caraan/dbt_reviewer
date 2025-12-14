## Triggering jobs in API from dbt

<img width="1394" height="287" alt="image" src="https://github.com/user-attachments/assets/8c342988-2fb7-4140-82ee-ec04361ae449" />

### Requirements
1. Account ID
2. Job ID
3. Tokens

### Personal Tokens

Personal tokens are tied to your own user. It'll add the same access as your user, which might not be enough or may be too much. This can be a bit dangerous sometimes if you use this API token for all your calls. Just be aware that if it's compromised, you might have to refresh it and a lot of your API calls might start to fail.

1. **Your name** --> **Your profile** --> **API tokens** --> **Personal tokens**

### Service Tokens

Service token may not be available for all users. If it's available, then you'll have the ability to look for existing ones and create new tokens.

**Creating a new Service Token**

<img width="667" height="384" alt="image" src="https://github.com/user-attachments/assets/e26e8612-c68f-4570-b013-05fd92f6eb25" />

1. Create button and provide it a name.
2. You can also add a permission set which is more granular than using the token for a specific user. Example - the scope you need to trigger job is having the role of a job admin, then you can also decide if this applies to all projects or specific projects only.
3. Copy your generated token.

Once you have your token, you are ready to trigger your job.

### Ways to Trigger your Job using API

**Curl**

This is a tool that's available in many machiens and it is quite a famous way to trigger or to call some APIs or to call some http addresses.

<img width="851" height="115" alt="image" src="https://github.com/user-attachments/assets/a3ca2916-a6b4-4f9c-b647-f89d6935957a" />

Enter the command as it is, then hit Enter. Verify if the status is successful. Then, refresh your run history and you'll see that your job is running.

**Python**

<img width="1099" height="733" alt="image" src="https://github.com/user-attachments/assets/fca9955d-0132-4a24-a439-943e4f1a0f1f" />

**dbt-cloud-cli**

Instead of providing the full URL of the API endpoint, we just need to provide our account ID, job ID, and the cause.

<img width="840" height="506" alt="image" src="https://github.com/user-attachments/assets/00f9bd3f-3f14-4dde-bbb8-f00dceeb393e" />
