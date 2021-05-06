# Creating struct type in golang

#### Creating [struct](https://medium.com/rungo/structures-in-go-76377cc106a2)

```go
type CreateAccountRequest struct {
	Type           string            `json:"type"`
	Id             string            `json:"id"`
	OrganisationId string            `json:"organisation_id"`
	Attributes     AccountAttributes `json:"attributes"`
}
```

It was interesting that property name, type, and json format are all specified and separated by spaces

