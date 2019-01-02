# Serverless Python Sample
[![serverless](http://public.serverless.com/badges/v3.svg)](http://www.serverless.com)

# serverlessを覚える

- cloneする

```
$ git clone git@github.com:yfujii01/serverless-python-sample.git
```

- Setupする

# Usage
## Setup
| **Step** | **Command** |**Description**|
|---|-------|------|
|  1. | `npm install -g serverless` | Install Serverless CLI  |
|  2. | `npm install` | Install Serverless dependencies  |
|  3. | Set up an AWS account with admin permissions | [Documentation](https://serverless.com/framework/docs/providers/aws/guide/credentials/)  |

- fishでvirtualenvを使う

以下を参考にインストールする

https://github.com/adambrenecki/virtualfish

環境を作る

| **Step** | **Command** |**Description**|
|---|-------|------|
|  1. | `vf new posts` | Create virtual environment|
|  2. | `pip install -r requirements.txt` | Install dependencies|



- テストする

```
$ python test.py
test.py:22: DeprecationWarning: Please use assertEqual instead.
  self.assertEquals(200, res['statusCode'])
..
----------------------------------------------------------------------
Ran 2 tests in 0.437s

OK
```

- serverless frameworkで動作確認する1

```
$ sls invoke local -f listPosts
DEBUG:root:calling https://jsonplaceholder.typicode.com/posts

DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): jsonplaceholder.typicode.com:443

DEBUG:urllib3.connectionpool:https://jsonplaceholder.typicode.com:443 "GET /posts HTTP/1.1" 200 None

{
    "statusCode": 200,
    "body": "[\n  {\n    \"userId\": 1
    :
    :
}
```

- serverless frameworkで動作確認する2

```
$ sls invoke local -f getPost -d '{"pathParameters":{"id":"1"}}'
DEBUG:root:calling https://jsonplaceholder.typicode.com/posts/1

DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): jsonplaceholder.typicode.com:443

DEBUG:urllib3.connectionpool:https://jsonplaceholder.typicode.com:443 "GET /posts/1 HTTP/1.1" 200 None

{
    "statusCode": 200,
    "body": "{\n  \"userId\": 1,\n  \"id\": 1,\n  \"title\": \"sunt aut facere repellat provident occaecati excepturi optio reprehenderit\",\n  \"body\": \"quia et suscipit\\nsuscipit recusandae consequuntur expedita et cum\\nreprehenderit molestiae ut ut quas totam\\nnostrum rerum est autem sunt rem eveniet architecto\"\n}"
}
```


A simple serverless python sample. The service is running on AWS Lambda using [Serverless Framework](https://github.com/serverless/serverless).

The service has a dependency on external package (`requests`) and it exposes 2 REST API endpoints:

| **Endpoint** |**Description**|
|-------|------|
| `GET /posts` | Retrieves a list of posts  |
| `GET /posts/{id}` | Retrieves a specific post (e.g. `GET /posts/5`) |


## Development
| **Step** | **Command** |**Description**|
|---|-------|------|
|  1. | `mkvirtualenv posts` | Create virtual environment (using [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/)) |
|  2. | `pip install -r requirements.txt` | Install dependencies|


## Deployment

	sls deploy

### Invocation

	curl <host>/posts
	curl <host>/posts/5

# Tips & Tricks

### `help` command
Just use it on anything:

	sls  help
or

	sls <command> --help

### `deploy function` command
Deploy only one function:

	sls deploy function -f <function-name>

### `logs` command
Tail the logs of a function:

	sls logs -f <function-name> -t

### `info` command
Information about the service (stage, region, endpoints, functions):

	sls info

### `invoke` command
Run a specific function with a provided input and get the logs

	sls invoke -f <function-name> -p event.json -l

# Credits
[JSONPlaceholder](https://jsonplaceholder.typicode.com) by [@typicode](https://github.com/typicode) is used for the posts backend.
