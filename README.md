# GAR Docker Repository Image Push Action

Google Artifact Registry (GAR) is a service available on the Google Cloud Platform (GCP). GAR Docker repositories are
one way to privately store Docker images.

**This action has not been endorsed by Google, its Parent Alphabet, or any related entity.**

This action encapsulates the steps needed to push a Docker image to a GAR repository.

## Features
- Minimal Configuration

## Usage

```yaml
...
    steps:
      - uses: actions/checkout@v3

      - name: Build Application
        run: "make build"
        
      - name: Build Docker Image
        run: |
          export TAG=`echo $GITHUB_REF | awk -F/ '{print $NF}'`
          docker build -t my-docker-image:"$TAG"
          

      - name: Store Image
        uses: firstmate-systems/gar-push-docker-image@v1
        with:
          DOCKER_IMAGE_NAME: "my-docker-image:"${{ env.TAG }}
          GCP_CREDENTIALS: ${{ secrets.GCP_CREDENTIALS }}
          GCP_PROJECT_ID: my-project-id
          GCP_REPO_NAME: 'my-docker-repo'
          GCP_REGION: us-west3
```

## Inputs

|       Input       |   Type   | Required |   Default   |                               Description                                |
|:-----------------:|:--------:|:--------:|:-----------:|:------------------------------------------------------------------------:|
 | DOCKER_IMAGE_NAME | `string` |   Yes    |             |                       Name of Image to Push to GAR                       |
|  GCP_CREDENTIALS  | `string` |   Yes    |             | Service Account Credentials in JSON format that have been Base64 Encoded |
|  GCP_PROJECT_ID   | `string` |   Yes    |             |           ID of Project that the GAR Repo is associated with.            |
|   GCP_REPO_NAME   | `string` |   Yes    |             |                     Name of Artifact Registry in GCP                     |
|    GCP_REGION     | `string` |    No    | `us-west3`  |           Name of GCP Region that Artifact Registry is Located           |

## Outputs

None right now. If you have a use case, you're welcome to contribute.

## License
[MIT License](LICENSE)