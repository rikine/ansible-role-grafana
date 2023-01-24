Role Name
=========

Grafana role for Ubuntu

Requirements
------------

Role Variables
--------------

    grafana_version: 9.3.2

    apt_additional_pkg:
      - adduser
      - libfontconfig1

    grafana_deb_pkg_url: "https://dl.grafana.com/oss/release/grafana_{{ grafana_version }}_amd64.deb"

    grafana_service:
      name: grafana-server
      enabled: true

    grafana_config_file:
      template: templates/grafana.ini.j2
      path: /etc/grafana/grafana.ini

    granafa_config: 
      http_addr: 0.0.0.0
      http_port: 3000
      users:
        allow_sign_up: false
      auth_anonymous:
        enabled: false

    grafana_url: "http://{{ granafa_config.http_addr }}:{{ granafa_config.http_port }}"
    grafana_api_url: "{{ grafana_url }}"

    grafana_security:
      admin_user: admin
      admin_password: admin

    grafana_datasources:
      - name: prometheus
        url: http://localhost:9090
        type: prometheus

    grafana_dashboards_dir: dashboards
    grafana_dashboards:
      - dashboard_id: 3662
        revision_id: 1
        datasource: prometheus
      - dashboard_id: 6671
        revision_id: 1
        datasource: prometheus

Dependencies
------------


Example Playbook
----------------

    - name: Setup Grafana
      hosts: grafana

      roles:
        - ansible-role-grafana

License
-------

BSD

Author Information
------------------

Anna Sheludchenko, ITMO University
