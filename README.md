# Veracode Auto Baseline Pipeline Scan Action

This action attempts to automatically download a baseline file from the baseline store for use in a Veracode Pipeline scan.

## Inputs

### Required Inputs

- `vid`: The Veracode ID.
- `vkey`: The Veracode API key.
- `file`: Filename of the packaged application to upload and scan.
- `token`: GitHub Access Token.

### Optional Inputs

- `source`: Name of the repository where the baseline will be stored. Default: `<owner>/veracode-baseline`.
- `result_file`: Specify the name of the results/baseline file (json) to read in. Default: `results.json`.
- `commit`: Custom commit message.
- `branch`: Override the default ref, which is the branch name.
- `repo`: Override the default repository. Default is `$GITHUB_REPOSITORY`.
- `checkbf`: Check if the baseline file to be pushed is new (less than 10 minutes old). Default: `True`.
- `update`: Whether a new baseline file should be pushed up to the repository. Default: `False`.
- `veracode_policy_name`: Name of the Veracode default policy or custom-built policy to apply to the scan results.
- `request_policy`: DEPRECATED, WILL BE REMOVED WITH NEXT VERSION - Name of the security policy to download as a file. Required only if you want to download the configuration for a custom policy defined by your organization. After downloading the policy, you can provide this file in a subsequent command using the policy_file parameter.
- `fail_on_severity`: Fail the pipeline job if the scan finds flaws of the specified severities. Enter a comma-separated list of severities in quotation marks.
- `fail_on_cwe`: Fail the pipeline job if the scan finds flaws of the specified CWEs. Enter a comma-separated list of CWE IDs.
- `baseline_file`: Filter the flaws that exist in the specified baseline file and show only the additional flaws in the current scan. Default: `.veracode-autobaseline/baseline.json`.
- `policy_name`: DEPRECATED, WILL BE REMOVED WITH NEXT VERSION - Name of the Veracode default policy rule to apply to the scan results. You can only use this parameter with a Veracode default policy.
- `policy_file`: Name of the local policy file you want to apply to the scan results.
- `timeout`: Amount of time, in minutes, for the Pipeline Scan to wait before reporting an unsuccessful scan if the scan does not complete. Default is 60 minutes, which is also the maximum value.
- `issue_details`: Enter true to show detailed messages for each issue in the results summary.
- `summary_display`: Enter true to show a human-readable results summary on the console. Default is true.
- `json_display`: Enter true to show the JSON containing the scan results on the console. Default is false.
- `verbose`: Enter true to display detailed messages in the scan results. Default is false.
- `summary_output`: Enter true to save the scan results as a human-readable file. Default is false.
- `summary_output_file`: Enter the filename of the scan results summary file. The file is stored in the current directory. Default is results.txt.
- `json_output`: Enter true to save the scan results in JSON format. Default is true.
- `json_output_file`: Rename the JSON file that contains the scan results. The file is stored in the current directory. Default filename is results.json.
- `filtered_json_output_file`: Enter the filename in the current directory to save results that violate pass-fail criteria. Default is filtered_results.json.
- `project_name`: Enter the name of the CI/CD code repository that runs a Pipeline Scan. This parameter adds the repository name to the scan results, which can help you track scans across repositories.
- `project_url`: Enter the source control URL for the CI/CD code repository that runs a Pipeline Scan.
- `project_ref`: Enter the source control reference, revision, or branch for the CI/CD code repository that runs a Pipeline Scan.

## Example Usage

```yaml
steps:
  - name: Check Baseline
    uses: wasptree/veracode-autobaseline@master
    with:
      token: ${{ inputs.token }}
      source: ${{ inputs.source }}
      file: ${{ inputs.result_file }}
      commit: ${{ inputs.commit }}
      branch: ${{ inputs.branch }}
      repo: ${{ inputs.repo }}
      checkbf: ${{ inputs.checkbf }}
      update: ${{ inputs.update }}

  - name: Run Veracode Pipeline Scan
    uses: veracode/Veracode-pipeline-scan-action@v1.0.12
    with:
      vid: ${{ inputs.vid }}
      vkey: ${{ inputs.vkey }}
      file: ${{ inputs.file }}
     
