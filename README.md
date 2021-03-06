# Flavio Espinoza Github Pages

```bash {.copy-clip}
sudo hello flavio :)
```
--
https://flavioespinoza.github.io

```javascript 
_createReservation (firstName, lastName, hotelName, arrivalDate, departureDate) {
    
    const _endpoint = 'https://us1.prisma.sh/public-luckox-377/reservation-graphql-backend/dev'

    axios({
        url: _endpoint,
        method: 'post',
        data: {
            query: `
                mutation {
                    createReservation(
                        data: {
                                name: "${firstName} ${lastName}" // <-- MUST USE DOUBLE QUOTES
                                hotelName: "${hotelName}"
                                arrivalDate: "${arrivalDate}"
                                departureDate: "${departureDate}"
                        }
                    )   {
                        id
                        name
                        hotelName
                        arrivalDate
                        departureDate
                    }
                }
        `
        }
    })
    .then(res => {
        let reservation = res.data.data.createReservation
        let confirmation = {
            confirm_arrivalDate: reservation.arrivalDate,
            confirm_departureDate: reservation.departureDate,
            confirm_hotelName: reservation.hotelName,
            confirm_id: reservation.id,
            confirm_name: reservation.name
        }
        this.setState(confirmation)
    })
    .catch(err => {
        console.error(err)
        alert(err.message)
    })
}
```