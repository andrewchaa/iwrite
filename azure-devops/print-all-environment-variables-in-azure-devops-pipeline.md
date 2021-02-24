# Print all environment variables in Azure DevOps pipeline

Sometimes, it's really handy to know what environment variables you have in the pipeline when things do go as planned and you need to debug it. Bash is available on every pipeline agent, so it's a safe option to try.

```yaml
steps: 
  – task: Bash@3
    inputs:
      targetType: 'inline'
      script: 'env | sort'
```

