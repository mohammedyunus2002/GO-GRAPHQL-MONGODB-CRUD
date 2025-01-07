# Setting Up a GraphQL Project with gqlgen

Follow these steps to create and set up your GraphQL project using `gqlgen`.

## 1. Create a New Folder for the Project

Run the following command to create a folder for your project:

```bash
mkdir gql-yt
```

## 2. Mod init your project, give it whatever name you like 
```bash
go mod init github.com/akhil/gql-yt
```

Get gql gen for your project 
```bash
go get github.com/99designs/gqlgen
```

## 3. Add gqlgen to tools.go 
```bash
printf '// +build tools\npackage tools\nimport _ "github.com/99designs/gqlgen"' | gofmt > tools.go
```

## 4. Get all the dependencies 
```bash
go mod tidy
```

## 5. Initialize your project 
```bash
go run github.com/99designs/gqlgen init
```

## 6. After you've written the graphql schema, run this - 
```bash
go run github.com/99designs/gqlgen generate
```
After you've built the project, these are the queries to interact with the API -
# Get All Jobs

```graphql
query GetAllJobs {
  jobs {
    _id
    title
    description
    company
    url
  }
}
```

# Create Job

```graphql
mutation CreateJobListing($input: CreateJobListingInput!) {
  createJobListing(input: $input) {
    _id
    title
    description
    company
    url
  }
}
```

{ "input": { "title": "Software Development Engineer - I", "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt", "company": "Google", "url": "www.google.com/" } }

# Get Job By Id

```graphql
query GetJob($id: ID!) {
  job(id: $id) {
    _id
    title
    description
    url
    company
  }
}
```

{ "id": "638051d7acc418c13197fdf7" }

# Update Job By Id

```graphql
mutation UpdateJob($id: ID!, $input: UpdateJobListingInput!) {
  updateJobListing(id: $id, input: $input) {
    title
    description
    _id
    company
    url
  }
}
```

{ "id": "638051d3acc418c13197fdf6", "input": { "title": "Software Development Engineer - III" } }

# Delete Job By Id

```graphql
mutation DeleteQuery($id: ID!) {
  deleteJobListing(id: $id) {
    deletedJobId
  }
}
```

{ "id": "638051d3acc418c13197fdf6" }
