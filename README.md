# Send


function Send-Order($json) {
    try {
        Invoke-RestMethod -Uri http://localhost:8080/api/orders -Method Post -ContentType "application/json" -Body $json
    } catch {
        "STATUS: " + [int]$_.Exception.Response.StatusCode
        $_.ErrorDetails.Message
    }
}

function Set-Status($id, $status) {
    Invoke-RestMethod -Uri "http://localhost:8080/api/orders/$id/status" -Method Patch -ContentType "application/json" -Body ('{"status":"' + $status + '"}')
}


$a = s '{"customerName":"Jan Kowalski","phoneNumber":"+48111111111","brand":"Toyota","model":"Corolla","vin":"JTDKB20U123456789","registrationNumber":"WA12345","mileage":120000,"faultDescription":"Brakes"}'
$b = s '{"customerName":"Anna Nowak","phoneNumber":"+48222222222","brand":"BMW","model":"X5","vin":"WBAKB81080CS12345","registrationNumber":"KR98765","mileage":85000,"faultDescription":"Engine light"}'
$c = s '{"customerName":"Jan Kowalski","phoneNumber":"+48111111111","brand":"Toyota","model":"Corolla","vin":"JTDKB20U123456789","registrationNumber":"WA12345","mileage":121500,"faultDescription":"Oil change"}'


Invoke-RestMethod -Uri "http://localhost:8080/api/orders/$($b.id)/status" -Method Patch -ContentType "application/json" -Body '{"status":"WAITING_FOR_PARTS"}'
Invoke-RestMethod -Uri "http://localhost:8080/api/public/track/$($a.accessCode)"

http://localhost:8080/api/orders
http://localhost:8080/api/orders?status=STATUS
http://localhost:8080/api/vehicles/search?q=VIN
http://localhost:8080/api/vehicles/search?q=NUMERSAMOCHODU
http://localhost:8080/api/public/track/ACCESSCODE
