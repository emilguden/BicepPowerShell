---
external help file: Bicep-help.xml
Module Name: Bicep
online version:
schema: 2.0.0
---

# Build-Bicep

## SYNOPSIS
Builds one or more .bicep files.

## SYNTAX

### Default (Default)
```powershell
Build-Bicep [[-Path] <String>] [[-OutputDirectory] <String>] [-ExcludeFile <String[]>]
 [-GenerateAllParametersFile] [-GenerateRequiredParametersFile] [-IgnoreDiagnostics] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

### OutputPath
```powershell
Build-Bicep [[-Path] <String>] [[-OutputPath] <String>] [-ExcludeFile <String[]>] [-GenerateAllParametersFile]
 [-GenerateRequiredParametersFile] [-IgnoreDiagnostics] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### AsHashtable
```powershell
Build-Bicep [[-Path] <String>] [-ExcludeFile <String[]>] [-AsHashtable] [-IgnoreDiagnostics] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### AsString
```powershell
Build-Bicep [[-Path] <String>] [-ExcludeFile <String[]>] [-AsString] [-IgnoreDiagnostics] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION
**Build-Bicep** is equivalent to the Bicep CLI command 'bicep build' but with some additional features.

- Compile all files in a directory  
- Generate ARM Template Parameter files  
- Output ARM Template directly as string or hashtable without writing to file  
  
Any error or warning from bicep will be written to the information stream.
To save output in a variable, use stream redirection. See example below.

## EXAMPLES

### Example 1: Compile single bicep file in working directory
```powershell
Build-Bicep -Path vnet.bicep
```

### Example 2: Compile single bicep file and specify the output directory
```powershell
Build-Bicep -Path 'c:\bicep\modules\vnet.bicep' -OutputDirectory 'c:\armtemplates\vnet.bicep'
```

### Example 3: Compile all .bicep files in a directory
```powershell
Build-Bicep -Path 'c:\bicep\modules\'
```

### Example 4: Compile all .bicep files in the working directory except vnet.bicep
```powershell
Build-Bicep -Path 'c:\bicep\modules\' -ExcludeFile vnet.bicep
```

### Example 5: Compile a .bicep file and output as string
```powershell
Build-Bicep -Path '.\vnet.bicep' -AsString
```

### Example 6: Compile a .bicep files in the working directory and generate a parameter file with all parameters
```powershell
Build-Bicep -Path '.\vnet.bicep' -GenerateAllParametersFile
```

### Example 7: Compile a .bicep files in the working directory and store diagnostic messages from bicep in a variable.
```powershell
$Diagnostics = Build-Bicep -Path '.\vnet.bicep' 6>&1
# Messages are tagged and can be sorted.
$Diagnostics | Where-Object Tags -eq 'Error'
$Diagnostics | Where-Object Tags -eq 'Warning'
```

Stores all Errors and Warnings from bicep in variable $Diagnostics.
Then outputs first all Errors then all Warnings.

### Example 8: Compile a .bicep file as hashtable and pass it to New-AzResourceGroupDeployment
```powershell
$Template=Build-Bicep -Path '.\vnet.bicep' -AsHashtable
New-AzResourceGroupDeployment -ResourceGroupName vnet-rg -TemplateObject $Template
```

### Example 9: Compiles single bicep file and saves the output as the specified file path.
```powershell
Build-Bicep -Path 'c:\bicep\modules\vnet.bicep' -OutputPath 'c:\armtemplates\newvnet.json'
```

### Example 10: Compile a .bicep and ignore all build warnings and errors
```powershell
Build-Bicep -Path '.\vnet.bicep' -IgnoreDiagnostics
```

## PARAMETERS

### -AsHashtable
The -AsHashtable prints all output as a hashtable instead of corresponding files.

```yaml
Type: SwitchParameter
Parameter Sets: AsHashtable
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -AsString
The -AsString prints all output as a string instead of corresponding files.

```yaml
Type: SwitchParameter
Parameter Sets: AsString
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ExcludeFile
Specifies a .bicep file to exclude from compilation

```yaml
Type: String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GenerateAllParametersFile
Generate an ARM template parameter file with all parameters from the bicep file.

```yaml
Type: SwitchParameter
Parameter Sets: Default, OutputPath
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -GenerateRequiredParametersFile
Generate an ARM template parameter file with the required parameters from the bicep file.

```yaml
Type: SwitchParameter
Parameter Sets: Default, OutputPath
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -IgnoreDiagnostics
Ignores all build warnings and errors.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OutputDirectory
Specfies the target directory where the compiled files should be created

```yaml
Type: String
Parameter Sets: Default
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -OutputPath
Specify the filename of the generated ARM template.

```yaml
Type: String
Parameter Sets: OutputPath
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path
Specfies the path to the directory or file that should be compiled

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: $pwd.path
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs. The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

## NOTES
Go to module repository https://github.com/PSBicep/PSBicep for detailed info, reporting issues and to submit contributions.

## RELATED LINKS
