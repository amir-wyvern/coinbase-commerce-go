[![Go Report Card](https://goreportcard.com/badge/github.com/benalucorp/coinbase-commerce-go)](https://goreportcard.com/report/github.com/benalucorp/coinbase-commerce-go)

![gdk](https://socialify.git.ci/benalucorp/coinbase-commerce-go/image?description=1&descriptionEditable=Accept%20cryptocurrency%20using%20Coinbase%20Commerce%20API.&font=Inter&logo=https%3A%2F%2Favatars.githubusercontent.com%2Fu%2F1885080%3Fs%3D280%26v%3D4&owner=1&pattern=Floating%20Cogs&theme=Light)

## Getting Started

Most requests to the Commerce API must be authenticated with an API key. You can create an API key in your Settings page after creating a [Coinbase Commerce](https://commerce.coinbase.com/signup) account.

## Installation

```shell
$ go get github.com/benalucorp/coinbase-commerce-go
```

## Charges

### [Create a charge](https://commerce.coinbase.com/docs/api/#create-a-charge)

```go
package main

import (
	"context"
	"log"
	"time"

	"github.com/benalucorp/coinbase-commerce-go"
	"github.com/benalucorp/coinbase-commerce-go/pkg/entity"
)

func main() {
	client, err := coinbase.NewClient(coinbase.Config{
		Key:              "REPLACE_WITH_YOUR_API_KEY",
		Timeout:          0,    // Default: 1 min.
		RetryCount:       0,    // Default: 0 = disable.
		RetryMaxWaitTime: 0,    // Default: 2 secs.
		Debug:            true, // Turn on on development for easier debugging.
	})
	if err != nil {
		log.Fatal(err)
	}

	resp, err := client.CreateCharge(context.Background(), &entity.CreateChargeReq{
		Name:        "The Sovereign Individual",
		Description: "Mastering the Transition to the Information Age",
		LocalPrice: entity.CreateChargePrice{
			Amount:   "100.00",
			Currency: "USD",
		},
		PricingType: "fixed_price",
		Metadata: entity.CreateChargeMetadata{
			CustomerID:   "id_1005",
			CustomerName: "Satoshi Nakamoto",
		},
		RedirectURL: "https://charge/completed/page",
		CancelURL:   "https://charge/canceled/page",
	})
	if err != nil {
		log.Fatal(err)
	}

	log.Printf("%+v", resp)
}
```


