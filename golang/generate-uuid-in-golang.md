# Generate UUID in golang

Unlike C\#, GO doesn't have built-in GUID type. So, use a third party package to create UUID

```bash
go get github.com/satori/go.uuid
```

```go
import (
	"fmt"
	"io"
	"os"

	"github.com/andrewchaa/form3client/services"
	uuid "github.com/satori/go.uuid"
)

func main() {

	accountId := uuid.NewV4()
	organisationId := uuid.NewV4()
```

It create UUID in UUID type. To call an API, I had to convert it to string.

```go
	createAccountRequest := struct {
		Data models.CreateAccountRequest `json:"data"`
	}{
		Data: models.CreateAccountRequest{
			Type:           "accounts",
			Id:             accountId.String(),
			OrganisationId: organisationId.String(),
			Attributes: models.AccountAttributes{
				Country:      country,
				BaseCurrency: baseCurrency,
				BankId:       bankId,
				BankIdCode:   bankIdCode,
				Bic:          bic,
			},
		},
	}

```

