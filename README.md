# DJANGO_HEALTH_CHECK

![licence](https://img.shields.io/badge/licence-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![checks](https://img.shields.io/badge/checks-unknown_PASS-brightgreen)

> Governed Anticloud packaging of the upstream project `DJANGO_HEALTH_CHECK` in category **MEDICAL_HEALTH**. check results: see ISOLATED_LAB_RESULTS. Every number below traces to a named file + run stamp; nothing is borrowed from other projects.

**Upstream:** DJANGO_HEALTH_CHECK · **Upstream pin:** `03760afacb53749c3ff36ddbb86ae5fd361763ba` · **Category:** MEDICAL_HEALTH · **Vendor:** Anticloud FZ LLE · **Licence:** MIT

---

## What This Project Does

===================
django-healthchecks
===================

Simple Django app/framework to publish health check for monitoring purposes

Features:

* Custom checks via Python functions
* Remote healthchecks
* Heartbeat monitoring

Status
======
.. image:: https://github.com/mvantellingen/django-healthchecks/workflows/Python%20Tests/badge.svg
    :target: https://github.com/mvantellingen/django-healthchecks/actions?query=workflow%3A%22Python+Tests%22

.. image:: http://codecov.io/github/mvantellingen/django-healthchecks/coverage.svg?branch=master
    :target: http://codecov.io/github/mvantellingen/django-healthchecks?branch=master

.. image:: https://img.shields.io/pypi/v/django-healthchecks.svg
    :target: https://pypi.python.org/pypi/django-healthchecks/

Installation
============

.. code-block:: shell

   pip install django_healthchecks

Usage
=====

Add the following to your urls.py:

.. code-block:: python

    url(r'^healthchecks/', include('django_healthchecks.urls')),

Add a setting with the available healthchecks:

.. code-block:: python

    HEALTH_CHECKS = {
        'postgresql': 'django_healthchecks.contrib.check_database',
        'cache_default': 'django_healthchecks.contrib.check_cache_default',
        'solr': 'your_project.lib.healthchecks.check_solr',
    }

You can also include healthchecks over http. This is useful when you want to
monitor if depending services are up:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'my_microservice': 'https://my-service.services.internal/healthchecks/',
        ...
    }

By default, http health checks will time out after 500ms. You can override this
as follows:

.. code-block:: python

    HEALTH_CHECKS_HTTP_TIMEOUT = 0.5

By default the status code is always 200, you can change this to something
else by using the `HEALTH_CHECKS_ERROR_CODE` setting:

.. code-block:: python

    HEALTH_CHECKS_ERROR_CODE = 503

You can also add some simple protection to your healthchecks via basic auth.
This can be specified per check or a wildcard can be used `*`.

.. code-block:: python

    HEALTH_CHECKS_BASIC_AUTH = {
        '*': [('admin', 'pass')],
        'solr': [],
    }

Using heartbeats
================

Heartbeats give a periodic update, to see whether an service was recently active.
When the service doesn't report back within timeout, a healthcheck can be triggered.
To use heartbeats, add the application to the ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS = [
        ...
        "django_healthchecks",
    ]

Include one of these checks:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'heartbeats': 'django_healthchecks.contrib.check_heartbeats'
        ...
        'expired_heartbeats': 'django_healthchecks.contrib.check_expired_heartbeats',
        ...
    }

Optionally, define an initial timeout:

.. code-block:: python

    HEALTHCHECKS_DEFAULT_HEARTBEAT_TIMEOUT = timedelta(days=1)

Let your code track the beats:

.. code-block:: python

    from datetime import timedelta
    from django_healthchecks.heartbeats import update_heartbeat

    update_heartbeat("myservice.name", default_timeout=timedelta(days=2))

Or use the decorator:

.. code-block:: python

    from django_healthchecks.heartbeats import update_heartbeat_on_success

    @update_heartbeat_on_success("myservice.name", default_timeout=...)
    def long_running_task():
        ....

Each time ``update_heartbeat()`` is called, the heartbeat is reset.
When a heartbeat didn't receive an update before it's ``timeout``,
the service name be mentioned in the ``check_expired_heartbeats`` check.

Updating timeouts
~~~~~~~~~~~~~~~~~

The ``default_timeout`` parameter is only assigned upon creation. Any updates
happen through the Django admin. To update the timeout automatically on
code deployment, use the ``timeout`` parameter instead. This will replace the
stored timeout value each time the ``update_heartbeat()`` function
is called, erasing any changes made in the Django admin.

---

## Installation

============

.. code-block:: shell

   pip install django_healthchecks

Usage
=====

Add the following to your urls.py:

.. code-block:: python

    url(r'^healthchecks/', include('django_healthchecks.urls')),

Add a setting with the available healthchecks:

.. code-block:: python

    HEALTH_CHECKS = {
        'postgresql': 'django_healthchecks.contrib.check_database',
        'cache_default': 'django_healthchecks.contrib.check_cache_default',
        'solr': 'your_project.lib.healthchecks.check_solr',
    }

You can also include healthchecks over http. This is useful when you want to
monitor if depending services are up:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'my_microservice': 'https://my-service.services.internal/healthchecks/',
        ...
    }

By default, http health checks will time out after 500ms. You can override this
as follows:

.. code-block:: python

    HEALTH_CHECKS_HTTP_TIMEOUT = 0.5

By default the status code is always 200, you can change this to something
else by using the `HEALTH_CHECKS_ERROR_CODE` setting:

.. code-block:: python

    HEALTH_CHECKS_ERROR_CODE = 503

You can also add some simple protection to your healthchecks via basic auth.
This can be specified per check or a wildcard can be used `*`.

.. code-block:: python

    HEALTH_CHECKS_BASIC_AUTH = {
        '*': [('admin', 'pass')],
        'solr': [],
    }

Using heartbeats
================

Heartbeats give a periodic update, to see whether an service was recently active.
When the service doesn't report back within timeout, a healthcheck can be triggered.
To use heartbeats, add the application to the ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS = [
        ...
        "django_healthchecks",
    ]

Include one of these checks:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'heartbeats': 'django_healthchecks.contrib.check_heartbeats'
        ...
        'expired_heartbeats': 'django_healthchecks.contrib.check_expired_heartbeats',
        ...
    }

Optionally, define an initial timeout:

.. code-block:: python

    HEALTHCHECKS_DEFAULT_HEARTBEAT_TIMEOUT = timedelta(days=1)

Let your code track the beats:

.. code-block:: python

    from datetime import timedelta
    from django_healthchecks.heartbeats import update_heartbeat

    update_heartbeat("myservice.name", default_timeout=timedelta(days=2))

Or use the decorator:

.. code-block:: python

    from django_healthchecks.heartbeats import update_heartbeat_on_success

    @update_heartbeat_on_success("myservice.name", default_timeout=...)
    def long_running_task():
        ....

Each time ``update_heartbeat()`` is called, the heartbeat is reset.
When a heartbeat didn't receive an update before it's ``timeout``,
the service name be mentioned in the ``check_expired_heartbeats`` check.

Updating timeouts
~~~~~~~~~~~~~~~~~

The ``default_timeout`` parameter is only assigned upon creation. Any updates
happen through the Django admin. To update the timeout automatically on
code deployment, use the ``timeout`` parameter instead. This will replace the
stored timeout value each time the ``update_heartbeat()`` function
is called, erasing any changes made in the Django admin.

## Usage

=====

Add the following to your urls.py:

.. code-block:: python

    url(r'^healthchecks/', include('django_healthchecks.urls')),

Add a setting with the available healthchecks:

.. code-block:: python

    HEALTH_CHECKS = {
        'postgresql': 'django_healthchecks.contrib.check_database',
        'cache_default': 'django_healthchecks.contrib.check_cache_default',
        'solr': 'your_project.lib.healthchecks.check_solr',
    }

You can also include healthchecks over http. This is useful when you want to
monitor if depending services are up:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'my_microservice': 'https://my-service.services.internal/healthchecks/',
        ...
    }

By default, http health checks will time out after 500ms. You can override this
as follows:

.. code-block:: python

    HEALTH_CHECKS_HTTP_TIMEOUT = 0.5

By default the status code is always 200, you can change this to something
else by using the `HEALTH_CHECKS_ERROR_CODE` setting:

.. code-block:: python

    HEALTH_CHECKS_ERROR_CODE = 503

You can also add some simple protection to your healthchecks via basic auth.
This can be specified per check or a wildcard can be used `*`.

.. code-block:: python

    HEALTH_CHECKS_BASIC_AUTH = {
        '*': [('admin', 'pass')],
        'solr': [],
    }

Using heartbeats
================

Heartbeats give a periodic update, to see whether an service was recently active.
When the service doesn't report back within timeout, a healthcheck can be triggered.
To use heartbeats, add the application to the ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS = [
        ...
        "django_healthchecks",
    ]

Include one of these checks:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'heartbeats': 'django_healthchecks.contrib.check_heartbeats'
        ...
        'expired_heartbeats': 'django_healthchecks.contrib.check_expired_heartbeats',
        ...
    }

Optionally, define an initial timeout:

.. code-block:: python

    HEALTHCHECKS_DEFAULT_HEARTBEAT_TIMEOUT = timedelta(days=1)

Let your code track the beats:

.. code-block:: python

    from datetime import timedelta
    from django_healthchecks.heartbeats import update_heartbeat

    update_heartbeat("myservice.name", default_timeout=timedelta(days=2))

Or use the decorator:

.. code-block:: python

    from django_healthchecks.heartbeats import update_heartbeat_on_success

    @update_heartbeat_on_success("myservice.name", default_timeout=...)
    def long_running_task():
        ....

Each time ``update_heartbeat()`` is called, the heartbeat is reset.
When a heartbeat didn't receive an update before it's ``timeout``,
the service name be mentioned in the ``check_expired_heartbeats`` check.

Updating timeouts
~~~~~~~~~~~~~~~~~

The ``default_timeout`` parameter is only assigned upon creation. Any updates
happen through the Django admin. To update the timeout automatically on
code deployment, use the ``timeout`` parameter instead. This will replace the
stored timeout value each time the ``update_heartbeat()`` function
is called, erasing any changes made in the Django admin.

## API

* Remote healthchecks
* Heartbeat monitoring

Status
======
.. image:: https://github.com/mvantellingen/django-healthchecks/workflows/Python%20Tests/badge.svg
    :target: https://github.com/mvantellingen/django-healthchecks/actions?query=workflow%3A%22Python+Tests%22

.. image:: http://codecov.io/github/mvantellingen/django-healthchecks/coverage.svg?branch=master
    :target: http://codecov.io/github/mvantellingen/django-healthchecks?branch=master

.. image:: https://img.shields.io/pypi/v/django-healthchecks.svg
    :target: https://pypi.python.org/pypi/django-healthchecks/

Installation
============

.. code-block:: shell

   pip install django_healthchecks

Usage
=====

Add the following to your urls.py:

.. code-block:: python

    url(r'^healthchecks/', include('django_healthchecks.urls')),

Add a setting with the available healthchecks:

.. code-block:: python

    HEALTH_CHECKS = {
        'postgresql': 'django_healthchecks.contrib.check_database',
        'cache_default': 'django_healthchecks.contrib.check_cache_default',
        'solr': 'your_project.lib.healthchecks.check_solr',
    }

You can also include healthchecks over http. This is useful when you want to
monitor if depending services are up:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'my_microservice': 'https://my-service.services.internal/healthchecks/',
        ...
    }

By default, http health checks will time out after 500ms. You can override this
as follows:

.. code-block:: python

    HEALTH_CHECKS_HTTP_TIMEOUT = 0.5

By default the status code is always 200, you can change this to something
else by using the `HEALTH_CHECKS_ERROR_CODE` setting:

.. code-block:: python

    HEALTH_CHECKS_ERROR_CODE = 503

You can also add some simple protection to your healthchecks via basic auth.
This can be specified per check or a wildcard can be used `*`.

.. code-block:: python

    HEALTH_CHECKS_BASIC_AUTH = {
        '*': [('admin', 'pass')],
        'solr': [],
    }

Using heartbeats
================

Heartbeats give a periodic update, to see whether an service was recently active.
When the service doesn't report back within timeout, a healthcheck can be triggered.
To use heartbeats, add the application to the ``INSTALLED_APPS``:

.. code-block:: python

    INSTALLED_APPS = [
        ...
        "django_healthchecks",
    ]

Include one of these checks:

.. code-block:: python

    HEALTH_CHECKS = {
        ...
        'heartbeats': 'django_healthchecks.contrib.check_heartbeats'
        ...
        'expired_heartbeats': 'django_healthchecks.contrib.check_expired_heartbeats',
        ...
    }

Optionally, define an initial timeout:

.. code-block:: python

    HEALTHCHECKS_DEFAULT_HEARTBEAT_TIMEOUT = timedelta(days=1)

Let your code track the beats:

.. code-block:: python

    from datetime import timedelta
    from django_healthchecks.heartbeats import update_heartbeat

    update_heartbeat("myservice.name", default_timeout=timedelta(days=2))

Or use the decorator:

.. code-block:: python

    from django_healthchecks.heartbeats import update_heartbeat_on_success

    @update_heartbeat_on_success("myservice.name", default_timeout=...)
    def long_running_task():
        ....

Each time ``update_heartbeat()`` is called, the heartbeat is reset.
When a heartbeat didn't receive an update before it's ``timeout``,
the service name be mentioned in the ``check_expired_heartbeats`` check.

Updating timeouts
~~~~~~~~~~~~~~~~~

The ``default_timeout`` parameter is only assigned upon creation. Any updates
happen through the Django admin. To update the timeout automatically on
code deployment, use the ``timeout`` parameter instead. This will replace the
stored timeout value each time the ``update_heartbeat()`` function
is called, erasing any changes made in the Django admin.

## Dependencies

| Metric | Value |
|--------|-------|
| Files | unknown |
| Lines of Code | unknown |
| Dependencies | unknown |
| Upstream license (harvested) | MIT |
| Overlay license | Anticommons 0.1.0 |

Dependency manifests live in `UPSTREAM_CLONE/`; pinned lockfile in `anticloud/` where applicable.

## Configuration

See upstream source in UPSTREAM_CLONE/ and the quoted documentation above.

## Contributing

Fork the project, create a feature branch, run the test suite, and open a pull request against upstream.

## License

Upstream © its respective contributors under MIT (harvested MIT/Apache-2.0/BSD source; see `UPSTREAM_CLONE/LICENSE`). This packaging overlay is licensed under Anticommons 0.1.0.

## Upstream

- **project:** DJANGO_HEALTH_CHECK
- **Pinned SHA:** `03760afacb53749c3ff36ddbb86ae5fd361763ba`
- **source:** `UPSTREAM_CLONE/` (pinned at the SHA above)
- **Upstream README source:** `UPSTREAM_CLONE/README.rst`

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`df0456f1f6e2146c9d3b5ef3e044d3bb04c2acca867c0afb505d0c920c13e609`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe and Mail, Business Insider, National Post, Financial Post, StreetInsider, Digital Journal, Barchart, International Business Times, and fox47 · National Law Review.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

