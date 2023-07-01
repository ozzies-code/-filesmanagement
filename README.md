# -filesmanagement
This application performs file management in windows: copying, moving or deleting files.
Visual Basic 2005.NET 

Public Class FormPrincipal

    Private Sub BtnAbrirArchivo_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles BtnAbrirArchivo.Click
        OpenFileDialog1.InitialDirectory = "C:\"
        OpenFileDialog1.Title = "Seleccione un archivo"
        OpenFileDialog1.FileName = ""

        If OpenFileDialog1.ShowDialog <> Windows.Forms.DialogResult.Cancel Then
            TxtOrigen.Text = OpenFileDialog1.FileName
        Else
            TxtOrigen.Text = ""

        End If
    End Sub

    Private Sub BtnGuardarArchivo_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles BtnGuardarArchivo.Click
        SaveFileDialog1.Title = "Especifique el nombre del archivo de destino"
        SaveFileDialog1.Filter = "Archivos de texto (*.txt)|*.txt"
        SaveFileDialog1.FilterIndex = 1
        SaveFileDialog1.OverwritePrompt = True

        If SaveFileDialog1.ShowDialog <> Windows.Forms.DialogResult.Cancel Then
            TxtDestino.Text = SaveFileDialog1.FileName
        End If
    End Sub

    Private Function ExisteArchivoOrigen() As Boolean
        If Not (System.IO.File.Exists(TxtOrigen.Text)) Then
            MessageBox.Show("El Archivo No Existe")
            Return False
        Else
            Return True
        End If
    End Function

    Private Sub BtnCopiarArchivo_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles BtnCopiarArchivo.Click
        If Not (ExisteArchivoOrigen()) Then Exit Sub
        System.IO.File.Copy(TxtOrigen.Text, TxtDestino.Text)
        MessageBox.Show("Se ha copiado correctamente el archivo.")
    End Sub

    Private Sub BtnMoverArchivo_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles BtnMoverArchivo.Click
        If Not (ExisteArchivoOrigen()) Then Exit Sub
        System.IO.File.Move(TxtOrigen.Text, TxtDestino.Text)
        MessageBox.Show("Se ha movido correctamente el archivo.")
    End Sub

    Private Sub BtnBorrarArchivo_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles BtnBorrarArchivo.Click
        If Not (ExisteArchivoOrigen()) Then Exit Sub
        If MessageBox.Show("¿Esta seguro que desea borrar " & "el archivo de origen?", "Mi App", MessageBoxButtons.YesNo, MessageBoxIcon.Question) = Windows.Forms.DialogResult.Yes Then

            System.IO.File.Delete(TxtOrigen.Text)
            MessageBox.Show("Se ha borrado correctamente el archivo.")

        End If
    End Sub

    Private Sub FormPrincipal_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load

    End Sub
End Class

