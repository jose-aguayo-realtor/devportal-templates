# Migration Results

## Basic Information
- **Repository:** {{ values.repository }}
- **Organization:** {{ values.organization }}
- **Dry Run:** {{ values.dryRun ? 'Yes' : 'No' }}
- **Status:** {{ steps.call_migrate_endpoint.output.data.status }}
- **Request ID:** {{ steps.call_migrate_endpoint.output.data.request_id }}
- **HTTP Code:** {{ steps.call_migrate_endpoint.output.code }}

## Message
{{ steps.call_migrate_endpoint.output.data.message }}

## Environment Results Summary

| Environment | Vault Env | Secrets Found | Copied | Status |
|-------------|-----------|---------------|---------|--------|
| 🔧 Development | {{ steps.call_migrate_endpoint.output.data.data.dev.vault_env }} | {{ steps.call_migrate_endpoint.output.data.data.dev.secrets_found }} | {{ steps.call_migrate_endpoint.output.data.data.dev.copied ? 'Yes' : 'No' }} | {{ steps.call_migrate_endpoint.output.data.data.dev.error ? '❌ Error' : '✅ OK' }} |
| 🧪 Staging | {{ steps.call_migrate_endpoint.output.data.data.stag.vault_env }} | {{ steps.call_migrate_endpoint.output.data.data.stag.secrets_found }} | {{ steps.call_migrate_endpoint.output.data.data.stag.copied ? 'Yes' : 'No' }} | {{ steps.call_migrate_endpoint.output.data.data.stag.error ? '❌ Error' : (steps.call_migrate_endpoint.output.data.data.stag.secrets_found > 0 ? '✅ OK' : '⚠️ No Secrets') }} |
| 🚀 Production | {{ steps.call_migrate_endpoint.output.data.data.prod.vault_env }} | {{ steps.call_migrate_endpoint.output.data.data.prod.secrets_found }} | {{ steps.call_migrate_endpoint.output.data.data.prod.copied ? 'Yes' : 'No' }} | {{ steps.call_migrate_endpoint.output.data.data.prod.error ? '❌ Error' : '✅ OK' }} |

## Detailed Environment Information

### 🔧 Development Environment
- **Vault Environment:** {{ steps.call_migrate_endpoint.output.data.data.dev.vault_env }}
- **Secrets Found:** {{ steps.call_migrate_endpoint.output.data.data.dev.secrets_found }}
- **Copied:** {{ steps.call_migrate_endpoint.output.data.data.dev.copied ? 'Yes' : 'No' }}
{% if steps.call_migrate_endpoint.output.data.data.dev.secret_keys %}
- **Secret Keys:**
{% for key in steps.call_migrate_endpoint.output.data.data.dev.secret_keys %}
  - `{{ key }}`
{% endfor %}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.dev.error %}
- **❌ Error:** {{ steps.call_migrate_endpoint.output.data.data.dev.error }}
{% endif %}

### 🧪 Staging Environment
- **Vault Environment:** {{ steps.call_migrate_endpoint.output.data.data.stag.vault_env }}
- **Secrets Found:** {{ steps.call_migrate_endpoint.output.data.data.stag.secrets_found }}
- **Copied:** {{ steps.call_migrate_endpoint.output.data.data.stag.copied ? 'Yes' : 'No' }}
{% if steps.call_migrate_endpoint.output.data.data.stag.message %}
- **Message:** {{ steps.call_migrate_endpoint.output.data.data.stag.message }}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.stag.secret_keys %}
- **Secret Keys:**
{% for key in steps.call_migrate_endpoint.output.data.data.stag.secret_keys %}
  - `{{ key }}`
{% endfor %}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.stag.error %}
- **❌ Error:** {{ steps.call_migrate_endpoint.output.data.data.stag.error }}
{% endif %}

### 🚀 Production Environment
- **Vault Environment:** {{ steps.call_migrate_endpoint.output.data.data.prod.vault_env }}
- **Secrets Found:** {{ steps.call_migrate_endpoint.output.data.data.prod.secrets_found }}
- **Copied:** {{ steps.call_migrate_endpoint.output.data.data.prod.copied ? 'Yes' : 'No' }}
{% if steps.call_migrate_endpoint.output.data.data.prod.secret_keys %}
- **Secret Keys:**
{% for key in steps.call_migrate_endpoint.output.data.data.prod.secret_keys %}
  - `{{ key }}`
{% endfor %}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.prod.error %}
- **❌ Error:** {{ steps.call_migrate_endpoint.output.data.data.prod.error }}
{% endif %}

---

{% if steps.call_migrate_endpoint.output.data.data.dev.error or steps.call_migrate_endpoint.output.data.data.stag.error or steps.call_migrate_endpoint.output.data.data.prod.error %}
## ⚠️ Errors Summary
{% if steps.call_migrate_endpoint.output.data.data.dev.error %}
- **Development:** {{ steps.call_migrate_endpoint.output.data.data.dev.error }}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.stag.error %}
- **Staging:** {{ steps.call_migrate_endpoint.output.data.data.stag.error }}
{% endif %}
{% if steps.call_migrate_endpoint.output.data.data.prod.error %}
- **Production:** {{ steps.call_migrate_endpoint.output.data.data.prod.error }}
{% endif %}
{% else %}
## ✅ No Errors Reported
All environments processed without errors.
{% endif %}

---

*Migration completed on {{ moment() | date('YYYY-MM-DD HH:mm:ss') }}*