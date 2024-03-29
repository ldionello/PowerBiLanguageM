//DI = Data Início
//DF = Data Fim

let dCalendario = (DI as date, DF as date) as table =>
let
    //Contar número de dias entre a data de início e fim
    Dias = Duration.Days(DF - DI) + 1,
    //Criando uma lista de datas
    Datas = List.Dates(DI, Dias, #duration(1, 0, 0, 0)),
    //Converter Lista em Tabela
    ListaparaTabela = Table.FromList(Datas, Splitter.SplitByNothing(), {"Data"}, null, ExtraValues.Error),
    AlterarTipo = Table.TransformColumnTypes(ListaparaTabela, {{"Data", type date}}),
    //Criando Colunas adicionais
    //Coluna Ano
    Ano = Table.AddColumn(AlterarTipo, "Ano", each Date.Year([Data]), Int64.Type),
    //Criando Trimestre
    Trimestre = Table.AddColumn(Ano, "Trimestre", each Number.ToText(Date.QuarterOfYear([Data])) & "T" & Number.ToText(Date.Year([Data])), type text),
    //Criando Semestre
    Semestre = Table.AddColumn(Trimestre, "Semestre", each Number.ToText(Number.RoundUp(Date.Month([Data])/6)) & "S" & Number.ToText(Date.Year([Data])), type text),
    //Número da Semana
    NumeroSemana = Table.AddColumn(Semestre, "Número Semana", each Date.WeekOfYear([Data]), Int64.Type),
    //Numero Mês
    MesNumero = Table.AddColumn(NumeroSemana, "Número Mês", each Date.Month([Data]), Int64.Type),
    DataINT = Table.AddColumn(MesNumero, "DateInt", each [Ano] * 100 + [Número Mês], Int64.Type),
    //Nome do Mes
    NomeMes = Table.AddColumn(DataINT, "Mês", each Date.ToText([Data], "MMM"), type text),
    MesMaiusculo = Table.TransformColumns(NomeMes, {{"Mês", Text.Proper, type text}}),
    //Dia da Semana
    DiaDaSemana = Table.AddColumn(MesMaiusculo, "Dia da Semana", each Date.ToText([Data], "dddd"), type text),
    //Mês-Ano
    MesAno = Table.AddColumn(DiaDaSemana, "Mês Ano", each Text.Combine({Text.From([Número Mês], "pt-BR"), Text.From([Ano], "pt-BR")}, "-"), type text)
in
    MesAno

in
    dCalendario
