# Spring Boot CI/CD Demo

A simple Spring Boot application with automated CI/CD pipeline using GitHub Actions and Railway deployment.

## Features

- Spring Boot 3.2.0 with Java 21
- REST API endpoints (`/api/hello` and `/api/health`)
- Automated testing with JUnit 5
- GitHub Actions CI/CD pipeline
- Railway deployment configuration

## API Endpoints

- `GET / api/hello` - Returns a greeting message with timestamp
- `GET /api/health` - Health check endpoint

## Local Development

### Prerequisites

- Java 21 or higher
- Maven 3.6 or higher

### Running the Application

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd cicd
   ```

2. Build and run the application:
   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

3. Access the application at `http://localhost:8080`

### Testing

Run the tests:
```bash
mvn test
```

## Railway Deployment

### Step 1: Create Railway Account

1. Go to [Railway.app](https://railway.app)
2. Sign up using your GitHub account
3. Verify your email address

### Step 2: Create New Project

1. Click "New Project" in Railway dashboard
2. Select "Deploy from GitHub repo"
3. Choose this repository
4. Railway will automatically detect it's a Java/Maven project

### Step 3: Configure Environment Variables

In Railway dashboard, go to your service settings and add:

- `PORT` - Railway will automatically set this
- `JAVA_VERSION` - Set to `21` (optional, Railway auto-detects)

### Step 4: Configure GitHub Secrets

1. Go to your GitHub repository
2. Navigate to Settings → Secrets and variables → Actions
3. Add the following secrets:

   - `RAILWAY_TOKEN`: Get this from Railway dashboard → Account → Tokens
   - `RAILWAY_SERVICE`: Your service name from Railway (usually auto-generated)

### Step 5: Enable GitHub Actions

1. Go to your GitHub repository
2. Navigate to Actions tab
3. Enable GitHub Actions if not already enabled
4. The workflow will automatically run on push to master branch

## CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/ci-cd.yml`) includes:

### Test Job
- Checks out code
- Sets up Java 21
- Caches Maven dependencies
- Runs tests
- Builds the application
- Uploads build artifacts

### Deploy Job (Main Branch Only)
- Runs after successful tests
- Builds the application
- Deploys to Railway using Railway CLI

## Deployment Process

1. **Push to master branch**: Triggers the CI/CD pipeline
2. **Tests run**: All tests must pass
3. **Build**: Application is built and packaged
4. **Deploy**: Application is automatically deployed to Railway
5. **Health check**: Railway verifies the application is running

## Monitoring

- Check deployment status in Railway dashboard
- View logs in Railway service logs
- Monitor GitHub Actions in the Actions tab
- Test endpoints: `https://your-app.railway.app/api/health`

## Troubleshooting

### Common Issues

1. **Build fails**: Check Java version compatibility
2. **Deploy fails**: Verify Railway token and service name
3. **App not starting**: Check Railway logs for startup errors
4. **Tests failing**: Run tests locally first

### Railway Logs

Access logs in Railway dashboard:
1. Go to your service
2. Click on "Deployments"
3. Select the latest deployment
4. View logs in the "Logs" tab

## Project Structure

```
cicd/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions workflow
├── src/
│   ├── main/
│   │   ├── java/com/example/cicddemo/
│   │   │   ├── CicdDemoApplication.java
│   │   │   └── controller/
│   │   │       └── HelloController.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/com/example/cicddemo/
│           └── controller/
│               └── HelloControllerTest.java
├── pom.xml                    # Maven configuration
├── railway.json              # Railway deployment config
├── nixpacks.toml            # Railway build config
└── README.md
```

## Next Steps

1. Customize the application endpoints
2. Add database integration
3. Implement authentication
4. Add monitoring and logging
5. Set up staging environment

## Support

For issues with:
- **Spring Boot**: Check [Spring Boot documentation](https://spring.io/projects/spring-boot)
- **Railway**: Check [Railway documentation](https://docs.railway.app)
- **GitHub Actions**: Check [GitHub Actions documentation](https://docs.github.com/en/actions)
