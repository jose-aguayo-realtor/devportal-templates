# Migration Results

## Summary
- **Organization**: {{ values.organization }}
- **Repository**: {{ values.repository }}
- **Dry Run**: {{ values.dryRun }}

## Migration Details
{% if steps.call_migrate_endpoint.output.success %}
✅ **Migration Status**: Successful
{% else %}
❌ **Migration Status**: Failed
{% endif %}

### Results:
{% if steps.call_migrate_endpoint.output.data %}
{% for item in steps.call_migrate_endpoint.output.data %}
- **Secret**: `{{ item.name }}`
  - Source: `{{ item.source }}`
  - Destination: `{{ item.destination }}`
  - Status: {{ item.status }}
{% endfor %}
{% else %}
No migration data available.
{% endif %}

### Additional Information:
{% if steps.call_migrate_endpoint.output.message %}
{{ steps.call_migrate_endpoint.output.message }}
{% endif %}

---
*Generated on: {{ moment() | date('YYYY-MM-DD HH:mm:ss') }}*