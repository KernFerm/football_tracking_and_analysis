# Security Policy

## Supported Versions

- Only the latest version of this project is actively supported and maintained for security updates.

## Reporting a Vulnerability

If you discover a security vulnerability, please report it by opening an issue or contacting the maintainer directly. Do **not** disclose security issues publicly until they have been addressed.

## Security Best Practices

- **Environment Variables:** All secrets (e.g., Flask secret key, JWT secret, database URI) must be set via environment variables or a `.env` file. Never hardcode secrets in the codebase.
- **Model Files:** Store model files (`.pt`) outside of public web roots. Do not commit sensitive or proprietary models to version control.
- **File Uploads:**
  - Only allow video files with safe extensions (`.mp4`, `.avi`, `.mov`, `.mkv`).
  - Uploaded files are saved with unique names using `secure_filename` to prevent overwriting and path traversal.
  - Uploaded files are stored in a dedicated folder, not the project root.
- **Database:**
  - Use an absolute path for the SQLite database URI.
  - Ensure the database file is not accessible from the public web root.
- **JWT Authentication:**
  - All API endpoints that modify or access user data require JWT authentication.
  - JWT tokens are signed with a strong secret key and have an expiration time (default: 60 minutes).
- **Dependencies:**
  - Use a virtual environment and keep dependencies up to date with `pip install -r requirements.txt`.
  - Review dependencies for known vulnerabilities.
- **Error Handling:**
  - All file I/O and model loading operations are wrapped in try/except blocks to prevent information leakage and crashes.
  - User-facing error messages do not reveal sensitive details.
- **CORS:**
  - CORS is restricted to trusted origins (default: `http://localhost:5173`).
- **Session Management:**
  - Sessions have a limited lifetime (default: 30 minutes).

## Additional Recommendations

- Run the application behind a secure reverse proxy (e.g., Nginx) in production.
- Use HTTPS for all API traffic.
- Regularly back up the database and model files.
- Monitor logs for suspicious activity.

## Responsible Disclosure

We appreciate responsible disclosure of security issues. Please give us a reasonable time to address any vulnerabilities before public disclosure.
