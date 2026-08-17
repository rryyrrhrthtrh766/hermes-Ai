---
name: wordpress-api-automation
description: Automating WordPress site management via REST API.
---
# WordPress Website Automation
Use when managing content, SEO, or updates on a WordPress site via API.

## Trigger Conditions
- Automating content publication, updating page content, or bulk edits on a WordPress site.
- Optimizing pages for SEO, such as text replacement, keyword insertion, or structure updates.

## Workflow
1. **Access**: Obtain username and Application Password from the user (from WordPress: Users > Profile > Application Passwords).
2. **Read**: Fetch existing page structure using GET to wp-json/wp/v2/pages/<id>.
3. **Analyze**: Check for page builders (e.g., Elementor). If Elementor is used, note that direct content field updates might not reflect in the visual builder; manual widget-level editing might be safer for complex layouts.
4. **Update**: Use a POST request to /wp-json/wp/v2/pages/<id> with Authorization: Basic <base64_encoded_creds>.
5. **Verify**: Perform a follow-up GET to verify status 200 and reflect the change.

## Pitfalls
- **Elementor vs. Gutenberg**: Editing the content field via API might not affect Elementor widgets. If updates fail to render visually, advise the user that manual widget-level update is necessary for structural integrity.
- **API Authorization**: Ensure the Application Password is used, not the login password. Ensure the user's role has sufficient permissions (administrator is preferred).
- **Network Security**: Some sites block automated tools (HTTP 403) or have strict WAFs. If 401 occurs, verify the role permission.
- **Content Formatting**: When replacing content via API, wrap the text in valid HTML.
