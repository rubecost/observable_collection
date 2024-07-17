# observable_collection
Uso de ObservableCollection com pacote CommunityToolkit.Mvvm para coleção de objetos na View em forma de Lista vertical.

## Model:
````CSharp
public class RegistroHistoricoModel
{
	public string? Nome_Usuario { get; set; }
	public string? Item_Atualizado { get; set; }
}
````
## ViewModel
````CSharp
using CommunityToolkit.Mvvm.ComponentModel;
using System.Collections.ObjectModel;
using MeuApp.Models;

internal class RegistroHistoricoViewModel : ObservableObject
{
    #region VARIAVEIS
    private ObservableCollection<RegistroHistoricoModel>? _registros;
    #endregion

    #region CONSTRUTOR
    public RegistroHistoricoViewModel()
    {
        Registros = new ObservableCollection<RegistroHistoricoModel>();
        CarregarregistrosDeExemplo();
    }
    #endregion

    #region OBJETOS
    public ObservableCollection<RegistroHistoricoModel> Registros
    {
        get => _registros ??= new ObservableCollection<RegistroHistoricoModel>();
        set => SetProperty(ref _registros, value);
    }
    #endregion

    #region PROCESSOS
// Inserindo dados de forma ficticia somente para demonstração, porém em um cenario real elas seriam otidas de alguma fonte externa atravez de requisições
    private void CarregarregistrosDeExemplo()
    {
        Registros = new ObservableCollection<RegistroHistoricoModel>
        {
            new RegistroHistoricoModel
            {
                Nome_Usuario = "Maria Gomes",
                Item_Atualizado = "Endereço",
            },
        };
    }
    #endregion
#region COMANDOS
#endregion
}

````
## View
````Xml
 <!--Fazendo um Binding da coleção de objetos Registros da ViewModel-->
 <CollectionView ItemsSource="{Binding Registros}">
     <CollectionView.ItemTemplate>
         <DataTemplate>
             <Grid ColumnDefinitions="*,*">
                 <Frame Grid.Column="0">
                     <!--Fazendo um Binding dos Objetos Nome_usuario e Item_Atualizado que pertencem a coleção Registros -->
                     <Label Text="{Binding Nome_Usuario}" />
                 </Frame>
                 <Frame Grid.Column="1">
                     <Label Text="{Binding Item_Atualizado}" />
                 </Frame>
             </Grid>
         </DataTemplate>
     </CollectionView.ItemTemplate>
 </CollectionView>
````
