```json

curl -X POST http://10.1.205.9:8080/uaz-rh/config/controlAcceso/usuarios/editarUsuario  -H "Content-Type: application/json" -d '{ "idUsuario": 1, "userName": "admin", "nombre": "FRIAS PACHECO OLIVER", "estatusMostrar": "ACTIVO", "email": "edgar.rzm@gmail.com" }'




curl -X POST "http://10.1.205.9:8080/uaz-rh/config/controlAcceso/usuarios/editarUsuario" -H "Content-Type: application/json" -d "{\"idUsuario\":1,\"userName\":\"admin\",\"password\":\"Gk9XcxWsUtM2oHC9TsnpUAoNeRKl93WrWjPIy0KEaAdap3kX4cHxUOfOxO8GoS59JD0CzpJRz9n9nAx3j5MbCg==\",\"idEmpleado\":1,\"matricula\":\"7578\",\"nombre\":\"FRIAS PACHECO OLIVER\",\"fechaCreacion\":\"2020-03-26T06:00:00.000Z\",\"estatus\":true,\"puesto\":\"Administrador del Sistema\",\"idPuesto\":1,\"email\":\"edgar.rzm@gmail.com\",\"idArea\":null,\"nombreArea\":null,\"esAdministrador\":true,\"primerIngreso\":false,\"idUnidad\":132,\"nombreUnidad\":\"INGENIERIA ELECTRICA PLANTEL ZACATECAS\",\"grupo\":\"Administrador\",\"idGrupo\":1,\"estatusMostrar\":\"ACTIVO\",\"rfc\":\"FIPO850602D88\"}"


```