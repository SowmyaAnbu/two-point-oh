# Two Point Oh!

A serverless web application that calculates the great-circle distance (in kilometers) between two geographic points. Enter the latitude and longitude for two locations, and the app plots them on a map and shows the distance between them.

## Architecture

The application runs entirely on AWS using a serverless architecture. A request flows left to right — from the user's browser through to the data layer — while IAM secures the permissions between each service.

| Service | Role |
|---------|------|
| **AWS Amplify** | Hosts the static web front end (HTML/CSS/JS) and serves it to the user. Connected to GitHub for continuous deployment — every push to the branch automatically redeploys the site. |
| **Amazon API Gateway** | Exposes a REST API endpoint. It receives the `POST` request from the front end (carrying the two coordinate pairs) and forwards it to the Lambda function. |
| **AWS Lambda** | Runs the function that calculates the distance between the two points and returns the result. No servers to provision or manage. |
| **Amazon DynamoDB** | Stores the distance results. After each calculation, the Lambda function writes the result to the table. |
| **AWS IAM** | Manages access securely, defining the roles and policies that allow each service to invoke the next — for example, permitting Lambda to write results to DynamoDB. |

## Tech stack

- **Front end:** HTML, CSS, JavaScript (Leaflet for the interactive map)
- **Hosting / CI-CD:** AWS Amplify + GitHub
- **API:** Amazon API Gateway (REST)
- **Compute:** AWS Lambda
- **Database:** Amazon DynamoDB
- **Security:** AWS IAM
