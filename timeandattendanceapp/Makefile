# Makefile for deploying the Flutter web projects to GitHub

BASE_HREF = $(OUTPUT)
APP_URL = https://timeandattendancedeployapp.pages.dev
# Replace this with your GitHub username
GITHUB_USER = psamx
GITHUB_REPO = git@github.com:psamx/TimeAndAttendanceDeployApp.git
BUILD_VERSION := $(grep 'version:' pubspec.yaml | awk '{print $$2}')

# Deploy the Flutter web project to GitHub
deploy:
ifndef OUTPUT
  $(error OUTPUT is not set. Usage: make deploy OUTPUT=<output_repo_name>)
endif

	@echo "Clean existing repository"
	flutter clean

	@echo "Getting packages..."
	flutter pub get

	@echo "Generating the web folder..."
	flutter create . --platform web
	@echo $(BASE_HREF)
	@echo "Building for web..."
	flutter build web --base-href $(BASE_HREF) --release

	@echo "Deploying to git repository"
	cd build/web && \
	git init && \
	git add . && \
	git commit -m "Deploy Version $(BUILD_VERSION)" && \
	git branch -M main && \
	git remote add origin $(GITHUB_REPO) && \
	git push -u -f origin main
	
	@echo "✅ Finished deploy: $(GITHUB_REPO)"
	@echo "🚀 Flutter web URL: $(APP_URL)"

.PHONY: deploy