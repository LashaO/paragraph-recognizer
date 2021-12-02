# paragraph-recognizer
Transcribes text from paragraph images. Built with Pytorch, TorchScript, Docker. Training experiments were tracked using Weights & Biases. Testing is done using Pytest.

Model weights can be downloaded from https://drive.google.com/drive/folders/1QnrqGOCIohpOTjkTCt86CrDDBXfkaeGv?usp=sharing. 

Part of my work for UC Berkeley's

## Build & Run
You can run the flask web server locally or in Docker
### Running locally
To start the server:
```
python api_server/app.py
```
Running inference on local files:
```
export API_URL=http://0.0.0.0:8000
(echo -n '{ "image": "data:image/png;base64,'$(base64 -w0 -i text_recognizer/tests/support/paragraphs/a01-077.png)'" }') | curl -X POST "${API_URL}/v1/predict" -H 'Content-Type: application/json' -d @-
```
Running inference on URLs:
```
curl "${API_URL}/v1/predict?image_url=https://fsdl-public-assets.s3-us-west-2.amazonaws.com/paragraphs/a01-077.png"
```
### Running in Docker
Building a docker image:
```
docker build -t text-recognizer/api-server -f api_server/Dockerfile .
```
Running the server:
```
docker run -p8000:8000 -it --rm text-recognizer/api-server
```
You can use the same scripts for running the inference in Docker.

### Testing
Basic tests can be run using:
```
pytest -s api_server/tests
```
