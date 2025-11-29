# Publishing Guide: Edmund's Claude Code Plugin

Complete step-by-step instructions for publishing your Claude Code plugin to GitHub and making it available for others to install.

## Prerequisites

- [ ] GitHub account
- [ ] Git installed locally
- [ ] Repository renamed to `edmunds-claude-code` ✅
- [ ] All configuration files updated ✅

## Step 1: Create GitHub Repository

### 1.1 Create New Repository on GitHub

1. Go to https://github.com/new
2. Fill in the details:
   - **Repository name**: `edmunds-claude-code`
   - **Description**: "Edmund's personal Claude Code setup with 14 productivity commands and 11 specialized AI agents for modern web development"
   - **Visibility**: Public (so others can install it)
   - **Initialize**: ❌ Don't add README, .gitignore, or license (we already have these)
3. Click "Create repository"

### 1.2 Push Your Local Repository

Once the GitHub repository is created, run these commands:

```bash
cd ~/Documents/GitHub/kenji-claude-code

# Add the GitHub remote
git remote add origin https://github.com/keeenjii/kenji-claude-code.git

# Push your code
git push -u origin main
```

If you encounter authentication issues:
- Use a Personal Access Token instead of password
- Or set up SSH keys (recommended): https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## Step 2: Verify Installation Works

Test that your plugin can be installed:

```bash
# Install from your GitHub repo
/plugin install keeenjii/kenji-claude-code

# Verify commands are available
/code-explain
/feature-plan

# Verify agents are available (they'll activate automatically based on context)
```

To uninstall and test again:
```bash
/plugin uninstall kenji-claude-code
```

## Step 3: Share Your Plugin

Your README already includes your GitHub username `keeenjii`, so users can copy-paste commands directly!

### Option A: Share Direct Installation Command

Share this command with others:

```bash
/plugin install keeenjii/kenji-claude-code
```

### Option B: Submit to Community Marketplaces

#### Claude Code Plugins Marketplace
1. Visit https://claudecodemarketplace.com/
2. Follow their submission guidelines
3. Share your plugin details

#### CC Plugins Curated Marketplace
1. Visit https://github.com/ccplugins/marketplace
2. Fork the repository
3. Add your plugin to their `marketplace.json`
4. Create a Pull Request with this format:

```json
{
  "name": "kenji-claude-code",
  "source": "keeenjii/kenji-claude-code",
  "description": "Personal Claude Code configuration",
  "version": "1.0.0",
  "author": "Kenji",
  "tags": ["productivity", "development"]
}
```

#### Claude Code Plugins Plus
1. Visit https://github.com/jeremylongshore/claude-code-plugins-plus
2. Follow their contribution guidelines
3. Submit your plugin details

### Versioning Guidelines

- **1.0.x** - Bug fixes and minor tweaks
- **1.x.0** - New commands or agents added
- **x.0.0** - Major restructuring or breaking changes

## Troubleshooting

### Issue: Plugin Won't Install

Check:
- Repository is public on GitHub
- `.claude-plugin/plugin.json` exists in the repo root
- JSON files have valid syntax (no trailing commas, proper quotes)

### Issue: Commands Don't Appear

Check:
- Command file paths in `plugin.json` match actual file locations
- Command files have `.md` extension
- Command files are not empty

### Issue: Agents Don't Activate

Check:
- Agent file paths in `plugin.json` match actual file locations
- Agent files have proper frontmatter with `name` and `description`
- Agents activate based on context, not commands

## Getting Help

If you run into issues:
- Claude Code Docs: https://docs.claude.com/en/docs/claude-code/plugin-marketplaces
- GitHub Issues: https://github.com/anthropics/claude-code/issues
- Community: Search for Claude Code plugins on GitHub

---

**Congratulations!** Once published, your plugin will be available for the Claude Code community to use and learn from. Happy sharing! 🎉
