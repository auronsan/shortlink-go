## About The Project

Shortlink App in Golang

* Multiple Node based Architecture to create and scale at ease
* Highly performant key-value storage system
* Centralized Storage option when multiple node created - requires tweaking.
* **API auth system not built**. Left for using it for your own use case like `JWT` or `paseto`. Self Implement.

Please see the `architecture` file in the repository on option you can use the app. For some minor tweaking may be required.

### Built With

List of Library and Framework used in building the app:

* [Gofiber](https://gofiber.io)
* [PogrebDB](github.com/dgraph-io/badger/v3)


<!-- GETTING STARTED -->
## Getting Started

Just download and run `go run main.go` and you are ready to go.

### Steps

Common Steps to Launch:

  ```sh
  go mod tidy
  go mod vendor
  go run main.go OR go build -ldflags "-s -w" main.go && ./main
  ```

### make `helper/constant.go` copy from `helper/constant.go.example`:

```
PORT            = 8080
Production      = 2 // Please set to 1 if in production.
Domain          = "http://localhost:8080/"
CookieName      = "local"
NodeID          = "N1|" // Increase per node by value as "N2|", "N3|"... for multiple node
DBFolder        = "./db/"
AddFromToken    = 3 // firt N character to get from token and use it in ShortID
ShortIDToken    = 7 // Further added from 1st N char of AddFromToken+NodeID: total=12
APIToken        = yoursecret
```

<details>
<summary>Click here to see Rest API Example:</summary>

  1. Short URL redirector: `/:short_code_here`
  2. API Routes:
>    - /api/create [Post]
>>     Takes `{"url": "https://github.com"}` with `Authorization: Bearer {APIToken}` from Header
>    - /api/update [Post]
>>     Takes `{"old": "https://github.com", "new": "https://bitbucket.com", "short": "shortcode"}` with `Authorization: Bearer {token}` from Header
>    - /api/delete [Post]
>>     Takes `{ "long": "https://bitbucket.com", "short": "shortcode"}` with `Authorization: Bearer {APIToken}` from Header
>    - /api/fetch [GET]
>>      Takes `Authorization: Bearer {APIToken}` from Header
>    - /api/fetch/:short_code_here [GET]
>>      {short_code_here} in the URL and Takes `Authorization: Bearer {APIToken}` from Header

**Note:** Remember to implement `Auth` system of your own and Replace `APITokenLength` check with your own function.
</details>

### Feature request?

Share your feature request via `issue` tracker.

### Feel like helping out:

- Via Code Contribution (if any / new feature)
- Star the repository and watch out for new updates and features.

### enable daemon systemd
- `go build`
- `chmod +x shortlink`
- add `shortlink.conf` 
WorkingDirectory=/home/dev/shortlink-go
ExecStart=/home/dev/shortlink-go/shortlink
- `systemctl daemon-reload`
- `systemctl start shortlink.conf`
- `systemctl enable shortlink.conf`

### Following Use cases:

- Self-Hosted URL tracking.
- Your URL tracking insights is in-house and not hosted or shared with third party.

<!-- LICENSE -->
## License

Distributed under the Apache License 2.0. See `LICENSE` for more information.


