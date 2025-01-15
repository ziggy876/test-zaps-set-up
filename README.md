# Personal Domain NIP-05 and LNURL Setup

https://www.youtube.com/watch?v=wJ32zo96LkU

This guide explains how to configure NIP-05 identifiers and LNURL for your domain using only DNS settings and the files in this GitHub repository without any command-line interactions.

## Prerequisites

- **Domain Name**: Ensure you own a domain name.
- **GitHub Account**: Have an active GitHub account.
- **GitHub Pages**: Familiarity with GitHub Pages for hosting static content.

## Repository Structure

This repository contains the following key files:

- `.well-known/nostr.json`: Defines NIP-05 identifiers.
- `.well-known/lnurlp/username`: Contains LNURL configuration for a specific user.
- `index.html`: A customizable landing page or redirect page.
- `.htaccess`: Handles URL redirections and headers.

## Steps to Set Up

### 1. Fork the Repository
   - Fork this repository to your GitHub account.

### 2. Modify Configuration Files
#### NIP-05 Identifier
   - Edit `.well-known/nostr.json` to include your Nostr public key and desired identifier.
   - **Important**: Your Nostr public key must be converted to a Hex key before using it in the `nostr.json` file.  
     - To convert your public key to Hex, visit [https://damus.io/key/](https://damus.io/key/).  
     - Enter your Nostr public key in the first box, and the Hex key will be displayed in the second box. Use this Hex key in your configuration.

#### LNURL Configuration
1. **Find Your LNURL File**:
   - Open `https://getalby.com/.well-known/lnurlp/<username>` in your browser.
   - Save this document to your local computer using `CTRL+S`.

2. **Edit the File**:
   - Remove the file extension (e.g., `.json`) from the saved file.
   - Your username is the part before the `@` in your Lightning address (e.g., `username@getalby.com`).
   - **Example**: If your LNURL is `example@getalby.com`, your username is `example`.
   - You should now have a file named `<username>` (no file extension) with contents similar to this:
     ```json
     {
       "status": "OK",
       "callback": "https://getalby.com/lnurl/callback/<username>",
       "tag": "payRequest",
       "maxSendable": 1000000,
       "minSendable": 1000,
       "metadata": "[[\"text/plain\",\"Payment to @<username>\"]]"
     }
     ```

3. **Update the File in the Repository**:
   - Navigate to the `.well-known/lnurlp/` folder in your GitHub repository.
   - Remove the old file (if one exists).
   - Upload the new `<username>` file (no file extension).

### 3. Customize the `index.html` Page
   - The `index.html` file serves as the main landing page for your domain.
   - By default, this page is set up to redirect visitors to a URL specified in the file. You can modify this URL to redirect users to any desired location.
   - **Advanced Option**: If you know HTML, you can fully customize this page to create a personalized landing page. Ensure the file is still named `index.html` for it to function as the default page for your domain.

### 4. Configure DNS Records
   - Access your domain registrar's DNS settings.
   - Add the following **A records**:
     - **Host**: `@`
     - **Values**:
       - `185.199.108.153`
       - `185.199.109.153`
       - `185.199.110.153`
       - `185.199.111.153`
   - These A records point your domain to GitHub Pages.

### 5. Set Up GitHub Pages
   - In your repository settings, enable GitHub Pages and set the source to the main branch.
   - Ensure your custom domain is correctly configured in the GitHub Pages settings.
   - Enable **forced HTTPS** in the GitHub Pages settings. This ensures that your website is served over a secure connection (HTTPS).  
     - **Note**: Your URL must use HTTPS to comply with NIP-05 and LNURL requirements.

### 6. Verify the Setup
   - After DNS propagation, verify the following:
     - NIP-05 setup: `https://yourdomain.com/.well-known/nostr.json`
     - LNURL configuration: `https://yourdomain.com/.well-known/lnurlp/<username>`
     - Landing page: `https://yourdomain.com`

## Notes

- **No Command-Line Required**: All configurations are managed through GitHub's web interface and your domain registrar's DNS settings.
- **DNS Propagation**: DNS changes may take up to 48 hours to propagate.
- **Security**: Ensure your `.well-known` files and `index.html` do not expose sensitive information.

For more details, refer to the [NIP-05 Specification](https://github.com/nostr-protocol/nips/blob/master/05.md) and [LNURL Documentation](https://github.com/lnurl/luds).

*Note: Replace placeholders like `yourdomain.com` and `username` with your actual domain and username.*
