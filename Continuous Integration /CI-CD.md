# Continuous Integration / CI-CD

- What is Continuous Integration / Delivery?
- Benefits of CI/CD in iOS
- Common CI/CD Tools
  - Fastlane
  - Bitrise
  - CircleCI
  - GitHub Actions
- Deployment
  - TestFlight
- Best Practices


## What is Continuous Integration / Delivery?

**CI/CD** is a software engineering practice where code changes are automatically built, tested, and prepared for release. It helps maintain code quality and accelerate the release process.

## Benefits of CI/CD in iOS

- Faster builds and deployments
- Automated testing
- Reduced manual errors
- Continuous feedback
- Simplified team collaboration

## Common CI/CD Tools

### Fastlane

Fastlane is an open-source tool that automates the release process.

**Use Cases:**
- Building and signing apps
- Uploading to TestFlight or App Store
- Managing screenshots and metadata

**Example Fastfile:**
```ruby
default_platform(:ios)

platform :ios do
  desc "Push a new beta build to TestFlight"
  lane :beta do
    increment_build_number
    build_app(scheme: "MyApp")
    upload_to_testflight
  end
end
```

---

### Bitrise

Bitrise is a CI/CD service built specifically for mobile apps.

**Features:**
- Visual workflows
- Supports iOS, Android, React Native, Flutter
- Integration with Fastlane and Slack

---

### CircleCI

CircleCI is a general-purpose CI/CD platform.

**Key Points:**
- Requires custom configuration with `.circleci/config.yml`
- Supports parallel testing and caching
- Integrates well with GitHub

---

### GitHub Actions

GitHub Actions allows you to automate workflows directly from your GitHub repo.

**Example Workflow:**
```yaml
name: iOS CI

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: macos-latest

    steps:
      - uses: actions/checkout@v2
      - name: Set up Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: 2.7

      - name: Install dependencies
        run: bundle install

      - name: Run Fastlane
        run: bundle exec fastlane beta
```

---

## Deployment

### TestFlight

TestFlight is Apple’s beta testing platform.

**How it works:**
- Upload app builds via Fastlane or Xcode
- Invite testers via email or public links
- Collect feedback before public release

---

## Best Practices

- Use version control for build configurations
- Keep secrets (API keys) secure using environment variables
- Run unit/UI tests on every build
- Use notifications (Slack, email) for build results
- Monitor crash logs post-release
