# Stocks

Stocks is a go library to get stock by symbol in from yahoo finance  

## Example

```
$ go get github.com/vic3lord/stocks
```

**Ex. 1**

```go
package main

import (
	"fmt"
	"github.com/vic3lord/stocks"
)

func main() {
	stock, err := stocks.GetQuote("goog")
	if err != nil {
		fmt.Println(err)
	}
	fmt.Printf("Google stock price is: %f", stock.GetPrice(0))
	stock.PrettyPrint()
}
```

**Ex. 2**

```go
package main

import (
	"fmt"
	"os"
	"os/signal"

	"github.com/vic3lord/stocks"
)

var input string

func main() {
	exit := make(chan os.Signal, 1)
	signal.Notify(exit, os.Interrupt)

	go func() {
		<-exit
		fmt.Println("Exiting...")
		os.Exit(0)
	}()

	Instruct()
	Prompt()
	GrabStock()
	for {
		stock, err := stocks.GetQuote(input)
		if err != nil {
			fmt.Println(err)
		}
		fmt.Printf("%s stock price is: %f\n", stock.GetName(), stock.GetPrice())
		Prompt()
		GrabStock()
	}
}

func Prompt() {
	fmt.Print("> ")
}

func Instruct() {
	fmt.Println("Press CTRL-C to exit!\nChoose stock symbol to get quote:")
}

func GrabStock() {
	fmt.Scanf("%s", &input)
}
```
## License

```
Copyright 2014 Or Elimelech

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
