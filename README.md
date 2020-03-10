# json
The json package is based on go1.13.8 encoding/json package, add one new function “json tag: must”
Sample Code:
-----------------------------------------------------------------------------------------------------------------------
package main

import (
        "github.com/DaoWind/json"
        "fmt"
)

type Msg struct {
        Bank       string `json:"bank,omitempty,must"`
        Code       string `json:"code,omitempty,must"`
        Version    string `json:"version,omitempty,must"`
        MsgId      string `json:"msgId,omitempty,must"`
}

// 1: Good example without error
var body = "{\"msgId\":\"202002280001\",\"bank\":\"102100009980\",\"version\":\"1.0.0\",\"code\":\"AsstRegr\"}"
// 2: Fail example with error(Field(code) Must Be Not-Empty!)
var body = "{\"msgId\":\"202002280001\",\"bank\":\"102100009980\",\"version\":\"1.0.0\",\"code\":\"\"}"
// 3: Fail example with error(Field(code) Must Be Exist!)
var body = "{\"msgId\":\"202002280001\",\"bank\":\"102100009980\",\"version\":\"1.0.0\"}"


func main() {
        var msg Msg
        err := json.Unmarshal([]byte(body), &msg)
        if err != nil {
                fmt.Printf("Got Error:%s\n", err.Error())
        } else {
                fmt.Printf("Success!\n")
        }
}
