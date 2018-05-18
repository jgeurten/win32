---
Description: 'Windows&\#160;HPC&\#160;Server&\#160;2008&\#160;R2 provides a way to simplify the creation of a custom diagnostic test that validates whether the result of the test matches the expected result on all of the nodes on which the test ran.'
audience: developer
author: 'REDMOND\\danlep'
manager: 'REDMOND\\timlt'
ms.assetid: 'd329b197-386d-4d0f-bb35-59f4e4f49678'
ms.prod: 'windows-server-dev'
ms.technology: 'compute-cluster-pack'
ms.tgt_platform: multiple
title: Steps for Creating a Custom Diagnostic Test that Checks that a Result Matches an Expected Value throughout an HPC Cluster
---

# Steps for Creating a Custom Diagnostic Test that Checks that a Result Matches an Expected Value throughout an HPC Cluster

Windows HPC Server 2008 R2 provides a way to simplify the creation of a custom diagnostic test that validates whether the result of the test matches the expected result on all of the nodes on which the test ran. To create this kind of diagnostic test, you include an [**AutoGenerateResult**](autogenerateresult.md) element in the XML file that defines the test, and designate the test type as Comparison. You also need to define a global parameter for the test that contains the value that the test should produce, and designate that parameter as the one that contains the expected value.

Windows HPC Server 2008 R2 does not restrict the Comparison test type to matching an exact expected value, but also supports matching a pattern for the expected value. You can specify that the test should match a pattern by using a .NET Framework regular expression for the value of the parameter that contains the expected value. For information about using .NET Framework regular expressions, see [.NET Framework Regular Expressions](http://go.microsoft.com/fwlink/p/?linkid=165378) (http://go.microsoft.com/fwlink/p/?linkid=165378).

When you designate a custom diagnostic test as a Comparison test, you do not need to implement a PostStep stage that compares the results from the different nodes to the expected value or pattern. The diagnostic service handles this comparison for you. The diagnostic service also automatically creates a report that summarizes whether the results matched the expected value for all of the nodes, and lists the results for all of the nodes.

This example creates a test that checks whether the version of Windows installed on the nodes matches the expected version, by using the **ver** command.

## Step 1: Create an XML file to define the custom test

The XML file in this example is similar to the ones in the examples in the [Steps for Creating a Custom Diagnostic Test that Runs an Existing Command](steps-for-creating-a-custom-diagnostic-test-that-runs-an-existing-command.md) and [Steps for Creating a Custom Diagnostic Test that Checks that a Result is Consistent throughout an HPC Cluster](steps-for-creating-a-custom-diagnostic-test-that-checks-that-a-result-is-consistent-throughout-an-hpc-cluster.md) topics. The unique items in the XML file this type of test include the following items:

-   The [**AutoGenerateResult**](autogenerateresult.md) element specifies a value of the **ExpectedValue** attribute, which specifies the global parameter that will contain the expected value for the test.

-   The [**Parameter**](parameter-element.md) element that defines the global parameter that specifies the expected result does not specify a value for the **Format** attribute. If you include a value for the **Format** attribute of the **Parameter** element for the parameter that you specify in the **ExpectedValue** attribute of the [**AutoGenerateResult**](autogenerateresult.md) element, an error occurs.

-   The [**Parameter**](parameter-element.md) element that defines the global parameter also specifies that the parameter should be used only in the PostStep stage by a specifying PostStep in the **UseOnlyInStep** attribute. You should specify a value for this attribute if you do not want to use the parameter that specifies the value for the comparison test as a parameter in the PreStep or RunStep command.

**To create an XML file that defines the custom test**

1.  In a text editor such as Notepad, paste the following text to define the metadata for the test.

    ```XML
    <DiagnosticTests>
        <DiagnosticTest
            Name="Windows Version Check"
            Description="Checks if the version of Windows matches the expected version."
            Company="Contoso, Ltd"
            Suite="Sample"
            Alias="WinVerCheck">
    
    ```

    

2.  After the text that you inserted in the previous step, paste the following text to define the parameter that will contain the expected value for the test.

    ```XML
            <Parameters>
                <Parameter Name="Version" SwitchName="Version" Type="String" Visibility="True" Description="The version of Windows that the nodes should have installed." DefaultValue="\nMicrosoft Windows \[Version 6.1.7600\]" UseOnlyInStep="PostStep"/>
            </Parameters>
    ```

    

    The default value for this parameter specifies a .NET Framework regular expression, so the test checks that result matches a pattern if the user runs the test with the default value. The .NET Framework regular expression includes character escapes because the output of the **ver** command begins with a newline character, and the opening bracket (\[) and closing bracket (\]) in the output of the command are special characters in the regular expression.

3.  After the text that you inserted in the previous step, paste the following text to designate the diagnostic test as a test that validates whether results of the test match the expected value on all of the nodes of the HPC cluster.

    ```XML
            <AutoGenerateResult TestType="Comparison" ExpectedValue="Version"/>
    ```

    

4.  After the text that you inserted in the previous step, paste the following text to define the command that the test will run.

    ```XML
            <RunStep Command="ver"/>
    
    ```

    

5.  After the text that you inserted in the previous step, paste the following text to add the necessary closing tags to create a valid XML file.

    ```XML
        </DiagnosticTest>
    </DiagnosticTests>
    ```

    

6.  Save the file as C:\\SampleTests\\WindowsVersion.xml on the head node of the HPC cluster.

## Step 2: Add the test to an HPC Cluster

In Windows HPC Server 2008 R2, you can add diagnostic tests to an HPC cluster by using HPC PowerShell or at the command prompt.

**To add a custom diagnostic test to an HPC cluster by using HPC PowerShell**

1.  On the head node, click **Start**, point to **All Programs**, click **Microsoft HPC Pack 2008 R2**, right-click **HPC PowerShell**, and then click **Run as administrator**.

2.  In **HPC PowerShell**, type the following cmdlet to add the test:

    **Add-HpcTest -File C:\\SampleTests\\WindowsVersion.xml**

    If you need to remove the test from the HPC cluster later, type the following cmdlet:

    **Remove-HpcTest -Alias WinVerCheck**

3.  Type the following cmdlet to verify that the test was added to the HPC cluster:

    **Get-HpcTest -Alias WinVerCheck**

4.  Type the following command to verify that the metadata and command for the test were correctly added to the HPC cluster:

    **Get-HpcTestDetail -Alias WinVerCheck**

**To add a custom diagnostic test to an HPC cluster at a command prompt**

1.  Open a command prompt window and type the following command to add the test:

    **test Add C:\\SampleTests\\WindowsVersion.xml**

    If you need to remove the test from the HPC cluster later, type the following command:

    **test Remove WinVerCheck**

2.  Type the following command to verify that the test was added to the HPC cluster:

    **test ListTests**

3.  Type the following command to verify that the metadata, parameters, and command for the test were correctly added to the HPC cluster:

    **test ViewTest WinVerCheck**

## Step 3: Run the test and view the results

After you add a custom diagnostic test to an HPC cluster, you can use HPC Cluster Manager, HPC PowerShell, or the command prompt window to run the test and view the results in the same way that you do for built-in diagnostic tests that Windows HPC Server 2008 R2 provides.

For information about using HPC Cluster Manager, see Overview of HPC Cluster Manager in the [HPC Cluster Manager Help](http://go.microsoft.com/fwlink/p/?linkid=124146) (http://go.microsoft.com/fwlink/p/?linkid=124146).

**To run the custom diagnostic test in HPC Cluster Manager**

1.  In **Diagnostics**, in the **Navigation Pane**, double-click **Tests** to display the list of companies that provided the diagnostic tests that are available on your HPC cluster, if the list is not already visible.

2.  Double-click **Contoso, Ltd** to display the list of suites, then click **Sample** to view the list of tests in the **Sample** suite.

3.  In the views pane, right-click the **Windows Version Check** test and click **Run**.

4.  In the **Run Diagnostic Tests** dialog box, select **All nodes** and click **Run**.

5.  If the **Run Test** dialog box appears, click **OK**.

### Additional considerations

To open **HPC Cluster Manager**, click **Start**, point to **All Programs**, click **Microsoft HPC Pack 2008 R2**, and then click **HPC Cluster Manager**. If the **User Account Control** dialog box appears, confirm that the action it displays is what you want, and then click **Continue**.

**To run the custom diagnostic test in HPC PowerShell or at a command prompt**

1.  In **HPC PowerShell**, type the following cmdlet:

    **Invoke-HpcTest -Alias WinVerCheck -NodeName** *list\_of\_nodes\_to\_run\_test*

    or

    At a command prompt, type the following command:

    **test run WinVerCheck -nodes:***list\_of\_nodes\_to\_run\_test*

2.  Note the run identifier that appears in the output of the cmdlet or at the command prompt so that you can view the results of the test later.

> [!Note]
>
> To specify parameter values for a diagnostic test in HPC PowerShell, use the *Parameters* parameter with a value that has the following format: @{*parameter\_name\_1*="*value1*"\[;*parameter\_name\_2*="*value2*";...\]}
>
> To specify a parameter value for a diagnostic test at the command prompt, include a parameter in the command with the following format: -*parameter\_name*:"*value"*

 

**To view the results of the custom test in HPC Cluster Manager**

1.  In **Diagnostics**, in the **Navigation Pane**, click **Test Results**.

2.  In the views pane, locate the test result for the **Windows Version Check** test and wait until the **State** for the result changes to **Success** or **Failure**.

3.  Click the test result for the **Windows Version Check** test.

4.  In the **Detail** pane, click the **Result** tab to view the report on the results for the diagnostic test. The report includes a **Summary** section that indicates whether the result of the command matched the expected value on all of the nodes, and a section for each node that shows the output of the command on that node.

**To view the results of the custom test in HPC PowerShell**

1.  In HPC PowerShell, type the following cmdlet to verify that the test finished and to see the overall results of the test.

    **Get-HpcTestResultDetail -RunId** *run\_identifier*

2.  Type the following cmdlet to export the report for the test run to a folder:

    **Export-HpcTestResult -RunId** *run\_identifier* **-Path C:\\SampleTests\\WindowsVersion**

3.  In Windows Explorer, navigate to C:\\SampleTests\\WindowsVersion and then double-click **Report.html**.

**To view the results of the custom test at a command prompt**

1.  Open a command prompt window ant type the following command to verify that the test finished and to see the overall results of the test.

    **test ViewRun** *run\_identifier*

2.  Type the following command to view the report for the test run:

    **test ViewResult** *run\_identifier*

 

 


