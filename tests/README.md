# Backend API tests

The backend test suite uses `pytest` and FastAPI's `TestClient`. Each test is
organized into Arrange, Act, and Assert sections. The client fixture restores
the in-memory activity data after each test so signup cases do not depend on
execution order or leave data changed for other tests.

## Scenarios covered

| Route | Scenario | Expected result |
| --- | --- | --- |
| `GET /` | Redirect to the frontend entry point | `307` with `Location: /static/index.html` |
| `GET /static/index.html` | Serve the frontend entry point | `200` with an HTML content type |
| `GET /activities` | Return the available activities | `200` with the activity data |
| `POST /activities/{activity_name}/signup?email=...` | Sign up a student | `200` and the student is added |
| `POST /activities/{activity_name}/signup?email=...` | Sign up an existing participant again | `400` |
| `POST /activities/{activity_name}/signup?email=...` | Sign up for an unknown activity | `404` |
| `POST /activities/{activity_name}/signup` | Omit the required email | `422` |

## Run the suite

Install the project requirements, then run:

```sh
python -m pytest
```
