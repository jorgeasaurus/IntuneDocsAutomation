# Microsoft Intune Updates Dashboard

A modern web dashboard that automatically tracks and displays the latest Microsoft Intune documentation updates from Microsoft Learn.

## 🚀 Features

- **Automated RSS Feed Updates**: GitHub Actions workflow downloads RSS data every 6 hours
- **Clean, Modern Design**: Responsive white/black design optimized for readability
- **Smart Categorization**: Automatically groups updates by type (Security, Apps, Devices, etc.)
- **GitHub Pages Ready**: Static site that works perfectly with GitHub Pages
- **No CORS Issues**: Uses local RSS file instead of external API calls

## 📋 Setup Instructions

### 1. Repository Setup
1. Fork or clone this repository
2. Push to your GitHub account
3. Enable GitHub Actions in your repository settings

### 2. GitHub Pages Setup
1. Go to your repository **Settings** → **Pages**
2. Under **Source**, select "Deploy from a branch"
3. Choose **main** branch and **/ (root)** folder
4. Click **Save**

### 3. GitHub Actions Permissions
1. Go to **Settings** → **Actions** → **General**
2. Under **Workflow permissions**, select "Read and write permissions"
3. Check "Allow GitHub Actions to create and approve pull requests"
4. Click **Save**

### 4. Initial Run
1. Go to **Actions** tab in your repository
2. Click on "Update Intune RSS Feed" workflow
3. Click **Run workflow** to trigger the first run manually

## 🔄 How It Works

### Automated Workflow
The GitHub Actions workflow (`.github/workflows/update-rss.yml`) automatically:

- **Downloads** the latest RSS feed from Microsoft Learn
- **Validates** the XML content
- **Checks** for changes since the last run
- **Commits** updated RSS file if changes are detected
- **Deploys** to GitHub Pages automatically

### Schedule
- **Every 6 hours**: Automatically checks for updates
- **Manual trigger**: Can be run manually from Actions tab
- **Push trigger**: Runs when workflow file is updated

### Files Generated
- `intune-rss.xml`: Latest RSS feed data
- `rss-metadata.json`: Metadata about the feed (update time, item count, etc.)

## 🎨 Customization

### Modify Update Categories
Edit the `categoryMapping` object in `index.html`:

```javascript
const categoryMapping = {
    'Security & Compliance': ['security', 'compliance', 'baseline'],
    'App Management': ['app', 'application', 'store'],
    // Add your own categories...
};
```

### Change Update Frequency
Modify the cron schedule in `.github/workflows/update-rss.yml`:

```yaml
schedule:
  # Every 3 hours instead of 6
  - cron: '0 */3 * * *'
```

### Styling
All CSS is embedded in `index.html` for easy customization. Key classes:
- `.header`: Main title section
- `.stats`: Statistics dashboard
- `.update-item`: Individual update cards
- `.category-title`: Category headers

## 🛠️ Local Development

### PowerShell Script
The repository also includes `intune_news_generator.ps1` for generating blog content:

```powershell
# Load the script
. .\intune_news_generator.ps1

# Generate blog post
Example-GenerateIntuneBlog -DaysBack 7

# Test RSS connectivity
Test-IntuneRSSFeed
```

### Local Web Server
To test the HTML page locally:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx http-server

# Then visit http://localhost:8000
```

## 📊 Sample Output

The dashboard displays:
- **Statistics**: Total updates, categories, latest update date
- **Categorized Updates**: Grouped by Security, Apps, Devices, etc.
- **Update Details**: Title, description, date, link to Microsoft Learn
- **Auto-refresh**: Manual refresh button for latest data

## 🔧 Troubleshooting

### Workflow Not Running
1. Check Actions permissions are set to "Read and write"
2. Verify GitHub Pages is enabled
3. Check the Actions tab for error logs

### No Data Showing
1. Wait for initial workflow run to complete
2. Check that `intune-rss.xml` file exists in repository
3. View browser console for error messages

### CORS Issues (Local Development)
- Use a local web server instead of opening HTML file directly
- The GitHub Pages deployment avoids CORS issues entirely

## 📝 File Structure

```
├── .github/
│   └── workflows/
│       └── update-rss.yml          # GitHub Actions workflow
├── ghost-exports/                  # Generated blog exports
├── index.html                      # Main dashboard page
├── intune_news_generator.ps1       # PowerShell blog generator
├── intune-rss.xml                  # RSS feed data (auto-generated)
├── rss-metadata.json              # Feed metadata (auto-generated)
└── README.md                       # This file
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test locally
5. Submit a pull request

## 📄 License

This project is open source and available under the MIT License.

## 🔗 Links

- [Microsoft Learn - Intune](https://learn.microsoft.com/en-us/intune/)
- [Official RSS Feed](https://docs.microsoft.com/api/search/rss?locale=en-us&facet=&%24filter=scopes%2Fany%28t%3A+t+eq+%27Intune%27%29)
- [GitHub Pages Documentation](https://pages.github.com/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)