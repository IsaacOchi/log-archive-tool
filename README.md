# Log Archive Tool

A command-line tool to compress and archive system logs automatically. This tool helps keep systems clean by archiving old logs in compressed format for future reference while freeing up space.

## Features

- ✅ Compress logs from any directory into tar.gz format
- ✅ Automatic timestamped archive naming (`logs_archive_YYYYMMDD_HHMMSS.tar.gz`)
- ✅ Centralized archive storage in `~/log-archives`
- ✅ Maintains archive operation log with timestamps
- ✅ Displays archive contents summary
- ✅ Shows archive size and file count
- ✅ Color-coded output for better readability
- ✅ Comprehensive error handling

## Installation

### Method 1: Quick Setup

1. Clone the repository:
```bash
git clone https://github.com/IsaacOchi/log-archive-tool.git
cd log-archive-tool
```

2. Make the script executable:
```bash
chmod +x log-archive
```

3. Run from the current directory:
```bash
./log-archive <log-directory>
```

### Method 2: System-Wide Installation

To use the tool from anywhere on your system:

```bash
sudo cp log-archive /usr/local/bin/
sudo chmod +x /usr/local/bin/log-archive
```

Now you can run it from any location:
```bash
log-archive <log-directory>
```

## Usage

### Basic Usage

```bash
log-archive <log-directory>
```

### Examples

**Archive application logs:**
```bash
log-archive ~/myapp/logs
```

**Archive system logs (requires sudo):**
```bash
sudo log-archive /var/log
```

**Archive specific service logs:**
```bash
sudo log-archive /var/log/nginx
```

## Sample Output

```
ℹ Log Archive Tool
==================================
ℹ Source Directory: /var/log/nginx
ℹ Archive Location: /home/user/log-archives/logs_archive_20240816_100648.tar.gz

ℹ Files to archive: 42

ℹ Creating archive...
✓ Archive created successfully!
ℹ Archive size: 2.3M
ℹ Archive location: /home/user/log-archives/logs_archive_20240816_100648.tar.gz

✓ Archive operation logged to: /home/user/log-archives/archive_log.txt

ℹ Archive Contents Summary:
==================================
nginx/
nginx/access.log
nginx/error.log
... and 39 more files

✓ Archive complete!

ℹ Recent Archive History:
==================================
2024-08-16 10:06:48 - Archived: /var/log/nginx -> logs_archive_20240816_100648.tar.gz (Size: 2.3M, Files: 42)

ℹ All archives are stored in: /home/user/log-archives
```

## How It Works

1. **Validates Input**: Checks if the specified directory exists and is readable
2. **Creates Archive Directory**: Creates `~/log-archives` if it doesn't exist
3. **Generates Timestamp**: Creates a unique filename with current date and time
4. **Compresses Logs**: Uses `tar` with gzip compression to create `.tar.gz` archive
5. **Logs Operation**: Records archive details to `archive_log.txt`
6. **Displays Summary**: Shows archive size, file count, and contents preview

## Archive Storage

- **Location**: All archives are stored in `~/log-archives/`
- **Naming**: `logs_archive_YYYYMMDD_HHMMSS.tar.gz`
- **Log File**: `~/log-archives/archive_log.txt` tracks all operations

## Prerequisites

- Linux or Unix-based operating system
- Bash shell
- `tar` command (pre-installed on most systems)
- Read permissions for the log directory (use `sudo` for system logs)

## Error Handling

The tool handles common errors:

- **No directory specified**: Shows usage information
- **Directory doesn't exist**: Displays error message
- **No read permissions**: Suggests using `sudo`
- **Archive creation fails**: Provides troubleshooting hints

## Extracting Archived Logs

To extract an archive:

```bash
# Navigate to archive directory
cd ~/log-archives

# Extract archive
tar -xzf logs_archive_20240816_100648.tar.gz

# View contents without extracting
tar -tzf logs_archive_20240816_100648.tar.gz
```

## Advanced Usage

### Automate with Cron

Schedule automatic log archiving:

```bash
# Edit crontab
crontab -e

# Archive logs daily at 2 AM
0 2 * * * /usr/local/bin/log-archive /var/log/myapp

# Archive logs weekly on Sunday at midnight
0 0 * * 0 /usr/local/bin/log-archive /var/log
```

### Clean Old Archives

Remove archives older than 30 days:

```bash
find ~/log-archives -name "logs_archive_*.tar.gz" -mtime +30 -delete
```

## Future Enhancements

Potential features for advanced versions:

- 🔄 Email notifications on archive completion
- ☁️ Upload to cloud storage (AWS S3, Google Cloud)
- 🔐 Encryption for sensitive logs
- 🗑️ Automatic cleanup of old archives
- 📊 Archive statistics and reporting
- 🔍 Search within archived logs
- 📅 Schedule-based archiving (built-in cron)

## Troubleshooting

**Permission Denied:**
```bash
sudo log-archive /var/log
```

**Archive Directory Full:**
```bash
# Check available space
df -h ~

# Clean old archives
rm ~/log-archives/logs_archive_2024*.tar.gz
```

**Command Not Found:**
```bash
# Ensure script is executable
chmod +x log-archive

# Or use absolute path
/path/to/log-archive <directory>
```

## Project Requirements

This project fulfills the requirements from https://roadmap.sh/projects/log-archive-tool:

- ✅ Accept log directory as command-line argument
- ✅ Compress logs in tar.gz format
- ✅ Store archives in new directory
- ✅ Log date and time of archive operation
- ✅ Use timestamped filenames

## Learning Objectives

This project teaches:

- Building CLI tools in Bash
- Working with files and directories
- Using the `tar` command for compression
- Date/time manipulation
- Error handling and validation
- User input processing
- File permissions and sudo usage

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/enhancement`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Created as part of the roadmap.sh DevOps learning path by Isaac Ochi.

## Project URLs

- **GitHub Repository**: https://github.com/IsaacOchi/log-archive-tool

---

⭐ If you find this project helpful, please star it on GitHub!
