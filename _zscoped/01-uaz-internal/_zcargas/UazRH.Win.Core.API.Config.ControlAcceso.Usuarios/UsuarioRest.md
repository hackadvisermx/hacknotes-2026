
```c#
// UazRH, Version=1.0.2.22, Culture=neutral, PublicKeyToken=null
// UazRH.Win.Core.API.Config.ControlAcceso.Usuarios.UsuarioRest
using System.Collections.Generic;
using System.Threading.Tasks;
using Exodo.SAL.Util;
using UazRH.Win.Core.API.Config.ControlAcceso.Usuarios;

public class UsuarioRest : ApiRestHttpClient
{
	private string url = "/config/controlAcceso/usuarios/";

	public async Task<List<Usuario>> listaEmpleados()
	{
		return await GetAsync<List<Usuario>>(url + "obtenerusuarios");
	}

	public async Task<List<Usuario>> listaEmpleadosActivos()
	{
		return await GetAsync<List<Usuario>>(url + "usuarioActivos");
	}

	public async Task<bool> cambiarContraseña(int? idUsuario, string newPassword)
	{
		UsuarioRest usuarioRest = this;
		string[] obj = new string[5] { url, "actualizarPassword/", null, null, null };
		int? num = idUsuario;
		obj[2] = num.ToString();
		obj[3] = "/";
		obj[4] = newPassword;
		return await usuarioRest.GetAsync<bool>(string.Concat(obj));
	}

	public async Task<Usuario> usuarioPorId(int? idUsuario)
	{
		UsuarioRest usuarioRest = this;
		string text = url;
		int? num = idUsuario;
		return await usuarioRest.GetAsync<Usuario>(text + num);
	}

	public async Task<Usuario> guardarUsuario(Usuario usuario)
	{
		return await PostAsync<Usuario>(url + "guardarUsuario", usuario);
	}

	public async Task<Usuario> editarUsuario(Usuario usuario)
	{
		return await PostAsync<Usuario>(url + "editarUsuario", usuario);
	}

	public async Task<bool> UsuarioHonorarioValidar(int? idUsuario)
	{
		UsuarioRest usuarioRest = this;
		string text = url;
		int? num = idUsuario;
		return await usuarioRest.GetAsync<bool>(text + "usuarioHonorarioValidar/" + num);
	}

	public async Task<bool> cambiarContraseñaPrimeraVez(CambiarClaveRequest request)
	{
		return await PostAsync<bool>(url + "cambiarContraseñaPrimeraVez", request);
	}
}

```