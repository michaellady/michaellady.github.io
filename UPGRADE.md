# Jekyll 4.4.1 Upgrade Guide

This document details the upgrade from Jekyll 4.3.3 to Jekyll 4.4.1 with Ruby 3.4.2.

## Upgrade Summary

**Previous Version:**
- Ruby: 3.3.x or earlier
- Jekyll: 4.3.3

**Current Version:**
- Ruby: 3.4.2
- Jekyll: 4.4.1

**Upgrade Date:** November 2025

## What Changed

### Ruby Version Upgrade

The site now requires **Ruby 3.4.2** or higher. Ruby 3.4.2 includes:
- Performance improvements
- Better memory management
- Security updates
- Enhanced compatibility with modern gems

### Jekyll Version Upgrade

Jekyll was upgraded from **4.3.3 to 4.4.1**. Key improvements in Jekyll 4.4.1:
- Bug fixes and stability improvements
- Better compatibility with Ruby 3.4+
- Performance optimizations
- Updated dependencies

### Dependencies Updated

All gem dependencies were updated to their latest compatible versions:
- `jekyll-archives` ~> 2.3
- `jekyll-sitemap` (latest)
- `jekyll-paginate` (latest)
- `base64`, `csv`, `json` (added as explicit dependencies for Ruby 3.4+)
- `ffi` >= 1.9.24 (security update)

## Migration Steps

If you're upgrading from the previous version, follow these steps:

### 1. Update Ruby Version

Install Ruby 3.4.2 using your preferred version manager:

**Using rbenv:**
```bash
rbenv install 3.4.2
rbenv local 3.4.2
```

**Using rvm:**
```bash
rvm install 3.4.2
rvm use 3.4.2
```

### 2. Update Gemfile

The `Gemfile` has been updated to specify Jekyll 4.4.1:

```ruby
source 'https://rubygems.org'
gem "jekyll", "~> 4.4.1"
gem "base64"
gem "csv"
gem "json"
gem 'jekyll-archives', '~> 2.3'
gem 'jekyll-sitemap'
gem 'jekyll-paginate'
gem "ffi", ">= 1.9.24"
```

### 3. Update .ruby-version

The `.ruby-version` file now specifies:
```
3.4.2
```

### 4. Update Dependencies

After updating Ruby and the Gemfile:

```bash
# Remove old Gemfile.lock
rm Gemfile.lock

# Install new dependencies
bundle install

# Verify versions
bundle exec jekyll --version  # Should show jekyll 4.4.1
ruby -v                       # Should show ruby 3.4.2
```

### 5. Update GitHub Actions Workflow

The `.github/workflows/jekyll.yml` file has been updated to use Ruby 3.4.2:

```yaml
- name: Setup Ruby
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: '3.4.2'
    bundler-cache: true
```

### 6. Test Locally

Before deploying, test the site locally:

```bash
# Build the site
bundle exec jekyll build

# Serve locally
bundle exec jekyll serve

# Test with production settings
JEKYLL_ENV=production bundle exec jekyll build
```

### 7. Commit and Deploy

Once testing is complete:

```bash
git add .ruby-version Gemfile Gemfile.lock .github/workflows/jekyll.yml
git commit -m "Upgrade to Jekyll 4.4.1 and Ruby 3.4.2"
git push origin master
```

GitHub Actions will automatically build and deploy the site.

## Breaking Changes

### Ruby 3.4.2 Changes

Ruby 3.4 requires explicit dependencies for some standard library gems that were previously bundled:
- `base64`
- `csv`
- `json`

These have been added to the `Gemfile` to prevent warnings and future compatibility issues.

### Jekyll 4.4.1 Changes

No breaking changes were encountered during the upgrade. Jekyll 4.4.1 is backward compatible with 4.3.3 for standard use cases.

## Compatibility Notes

### GitHub Pages

This site uses **GitHub Actions** for deployment, not the standard GitHub Pages build process. This allows us to:
- Use Jekyll 4.4.1 (GitHub Pages only supports 3.9.x)
- Use custom plugins like `jekyll-archives`
- Control the Ruby version
- Use the latest gem versions

The deployment is configured in `.github/workflows/jekyll.yml` and automatically runs on every push to the `master` branch.

### Plugins

All existing plugins continue to work with Jekyll 4.4.1:
- **jekyll-archives**: Works with custom build process
- **jekyll-sitemap**: Fully compatible
- **jekyll-paginate**: Fully compatible

### Themes

The Centrarium theme is compatible with Jekyll 4.4.1 without modifications.

## Troubleshooting

### Issue: "Your Ruby version is X.X.X, but your Gemfile specified 3.4.2"

**Solution:** Install and activate Ruby 3.4.2 using rbenv or rvm (see Migration Steps above)

### Issue: "Could not find gem 'jekyll (~> 4.4.1)'"

**Solution:**
```bash
bundle install
```

### Issue: "LoadError: cannot load such file -- base64"

**Solution:** The `base64`, `csv`, and `json` gems should be in your Gemfile. Run:
```bash
bundle install
```

### Issue: GitHub Actions build fails

**Solution:**
1. Ensure `.ruby-version` contains `3.4.2`
2. Ensure `Gemfile.lock` is committed to the repository
3. Check the workflow file specifies Ruby 3.4.2
4. Review GitHub Actions logs for specific errors

### Issue: Site builds locally but not in production

**Solution:** Test with production environment settings:
```bash
JEKYLL_ENV=production bundle exec jekyll build
```

Check for:
- Liquid syntax errors
- Missing front matter
- Path issues with assets

## Performance Improvements

After upgrading, you may notice:
- Faster build times (Ruby 3.4.2 performance improvements)
- Reduced memory usage
- More efficient gem loading
- Faster GitHub Actions deployments

## Security Improvements

The upgrade includes:
- Latest Ruby 3.4.2 security patches
- Updated `ffi` gem (>= 1.9.24) with security fixes
- Latest Jekyll 4.4.1 security updates
- Updated dependency versions with known vulnerability fixes

## Rollback Instructions

If you need to rollback to the previous version:

1. Revert the Ruby version:
```bash
rbenv local 3.3.0  # or your previous version
```

2. Revert Gemfile changes:
```ruby
gem "jekyll", "~> 4.3.3"
```

3. Update dependencies:
```bash
rm Gemfile.lock
bundle install
```

4. Revert workflow file:
```yaml
ruby-version: '3.3.0'
```

5. Test and commit:
```bash
bundle exec jekyll build
git add .
git commit -m "Rollback to Jekyll 4.3.3 and Ruby 3.3.0"
git push origin master
```

## Additional Resources

- [Jekyll 4.4.1 Release Notes](https://jekyllrb.com/news/)
- [Ruby 3.4.2 Release Notes](https://www.ruby-lang.org/en/news/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Jekyll Documentation](https://jekyllrb.com/docs/)

## Support

If you encounter issues not covered in this guide:
1. Check the [README.md](README.md) Troubleshooting section
2. Review GitHub Actions logs for deployment errors
3. Test locally with `bundle exec jekyll serve --verbose`
4. Check Jekyll documentation for version-specific changes

## Conclusion

The upgrade to Jekyll 4.4.1 and Ruby 3.4.2 provides:
- Improved performance
- Better security
- Enhanced compatibility
- Long-term support for future updates

The migration is straightforward with no breaking changes for standard Jekyll sites.
