# Ansible Role: Proxy

[![ubuntu-18](https://img.shields.io/badge/ubuntu-18.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![ubuntu-20](https://img.shields.io/badge/ubuntu-20.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg?style=flat)](https://opensource.org/licenses/MIT)
[![GitHub issues](https://img.shields.io/github/issues/OnkelDom/ansible-role-proxy?style=flat)](https://github.com/OnkelDom/ansible-role-proxy/issues)

## Description

Install and configure proxy applications

* Squid
* SquidGuard
* Dante Socks
* Proxy Pac/Wpad File
* Caddy Webserver

## Requirements

- Ansible >= 2.5 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `proxy_env` | {} | set proxy environment |
| `socks_enabled` | true | enable socks proxy |
| `socks_user` | proxy | default socks user |
| `socks_group` | proxy | default socks group |
| `socks_bind_ip` | "0.0.0.0" | default socks listen ip |
| `socks_port` | 1080 | default socks port |
| `socks_bind_external_interface` | "{{ ansible_default_ipv4.alias }}" | default external interface |
| `socks_debug` | "" | enable debug mode set to 1,2 or 3 is you need it |
| `socks_bind_ipv6_enabled` | false | enable socks ipv6 |
| `socks_bind_ipv6` | "::" | ipv6 bind ip |
| `socks_log_folder` | /var/log/danted | socks log folder |
| `socks_pid_folder` | /var/run/danted | socks pid folder |
| `socks_logrotate_days` | 14 | socks logrotate days |
| `socks_config` | /etc/danted.conf | socks config file |
| `socks_workers` | 4 | socks service workers |
| `socks_html_output` | true | socks generate config as html file |
| `socks_access_rules` | {} | define daccess rules - see [defaults/main.yml](defaults/main.yml) |
| `caddy_enabled` | true | enable caddy webserver |
| `caddy_group` | www-data | default caddy user |
| `caddy_user` | www-data | default caddy group |
| `caddy_logrotate_days` | 14 | caddy logrotate days |
| `caddy_web_path` | /var/www | caddy webserver basepath |
| `caddy_log_folder` | /var/log/caddy | caddy log folder |
| `caddy_basic_auth` | true | caddy enable basic auth |
| `caddy_basic_auth_user` | proxy | caddy basic auth user |
| `caddy_basic_auth_pass` | "JDJhJDE0JHI5Wlpua1BsQkF6M3o2TkpzclNmOU9JNHNabWY5V3ZkZHpkeEpIUWdaRFV2NDNyQS9oR3Zx" # pw: proxy | generate pass with caddy hash-password |
| `caddy_basic_auth_paths` | "/socks.html /squid.html /squid_acls /squidguard" | caddy define basic auth files |
| `caddy_forbidden_ips_text` | "IP-Address blocked" | caddy forbidden text |
| `caddy_forbidden_ips_enable` | true | caddy enable forbidden ips |
| `caddy_forbidden_ips` |  "" | caddy fordbidden ips/cidr to pac access |
| `caddy_allowed_ips_text` | "IP-Address not defined as allowed" | caddy not on allowed list text |
| `caddy_allowed_ips_enable` | true | caddy enable allowed ips |
| `caddy_allowed_ips` | "10.0.0.0/8 192.168.0.0/16 169.254.0.0/16" | caddy default allowed cidrs |
| `pac_enabled` | true | enable pac generation |
| `pac_file_proxys` | {} | pac defined proxyservers |
| `pac_file_rules` | {} | pac defined rules - see [defaults/main.yml](defaults/main.yml) |
| `squid_enabled` | true | enable squid proxy |
| `squid_html_output` | true | squid generate config as html file |
| `squid_user` | proxy | default squid user |
| `squid_group` | proxy | default squid group |
| `squid_logrotate_days` | 14 | squid logrotate days |
| `squid_log_folder` | /var/log/squid | squid log folder |
| `squid_pid_folder` | /var/run/squid | squid pid folder |
| `squid_config_dir` | /etc/squid | squid config folder |
| `squid_port` | 3128 | default squid port |
| `squid_logformat_name` | squid_json | default logformat name |
| `squid_logformat` | '{"proxy_squid_ip":"%la","proxy_squid_fqdn":"{{ansible_hostname }}.{{ansible_domain}}","proxy_client_ip":"%>a","proxy_client_fqdn":"%>A","proxy_user_agent":"%{User-Agent}>h","proxy_timestamp":"%tl","proxy_short_message":"%rm %ru HTTP/%rv","proxy_dst_host":"%{Host}>h","proxy_dst_ip":"%<a","proxy_dst_url":"%ru","proxy_http_status":"%>Hs","proxy_http_method":"%rm","proxy_http_referer":"%{Referer}>h","proxy_mime_content_type":"%mt","proxy_response_time":"%tr","proxy_request_size":"%>st","proxy_reply_size":"%<st","proxy_squid_request_status":"%Ss","proxy_squid_hierarchy_status":"%Sh"}' | json log format |
| `squid_url_rewrite_programm` | "/usr/bin/squidGuard -c {{ squid_config_dir }}/{{ squidguard_config_file }}" | squidguard rewrite program |
| `squid_url_rewrite_childen` | "25 startup=10 idle=10 concurrency=0" | squidguard rewrite childen |
| `squid_config_custom` | {} | squid custom config params - see [defaults/main.yml](defaults/main.yml) |
| `squid_config_refresh_pattern` | {} | squid refresh pattern - see [defaults/main.yml](defaults/main.yml) |
| `squid_ssl_ports` | [] | squid ssl ports list - see [defaults/main.yml](defaults/main.yml) |
| `squid_safe_ports` | [] | squid safe ports list - see [defaults/main.yml](defaults/main.yml) |
| `squid_src_acls` | {} | squid source acls - see [defaults/main.yml](defaults/main.yml) |
| `squid_dst_acls` | {} | squid destination acls - see [defaults/main.yml](defaults/main.yml) |
| `squidguard_enabled` | true | enable squidguard |
| `squidguard_html_output` | true | squidguard generate config as html file |
| `squidguard_log_folder` | /var/log/squidguard | squidguard log folder |
| `squidguard_script_dir` | /usr/local/bin/ | squidguard script dir |
| `squidguard_redirect_url` | "http://{{ ansible_hostname }}.{{ ansible_domain }}/cgi-bin/squidguard.cgi?clientaddr=%a&clientname=%n&clientuser=%i&srcclass=%s&targetclass=%t&url=%u" | squidguard redirect url |
| `squidguard_config_file` | squidguard.conf | squidguard config file |
| `squidguard_dbhome` | "{{ squid_config_dir }}/guard.d/blacklists" | squidguard dbhome folder |
| `squidguard_web_allow_all` | true | squidguard allow all websites after ruleset |
| `squidguard_blacklist_url` | "ftp://ftp.univ-tlse1.fr/pub/reseau/cache/squidguard_contrib/blacklists.tar.gz" | squidguard blacklist |
| `squidguard_blacklist` | {} | squidguard blacklist acls - see [defaults/main.yml](defaults/main.yml) |
| `squid_template` | false | enable squid custom error page templates |
| `squid_template_file` | squid.errors.client.html.j2 | squid define custom errorpage html file |
| `squid_template_errors` | {} | squid define errors - see [defaults/main.yml](defaults/main.yml) |

## Example

```yaml
---
- hosts: all
  roles:
  - ansible-role-proxy
  vars:
    #
    # Default settings
    #
    # Define proxy environment variables
    proxy_env: {}
    #  http_proxy: "http://proxy:3128"
    #  https_proxy: "http://proxy:3128"
    #  no_proxy: "localhost,127.0.0.1,.{{ ansible_domain }},10.0.0.0/8,192.168.0.0/16,169.254.0.0/16"
    #
    # Sockd default settings
    #
    socks_enabled: true
    socks_user: proxy
    socks_group: proxy
    socks_bind_ip: "0.0.0.0"
    socks_port: 1080
    socks_bind_external_interface: "{{ ansible_default_ipv4.alias }}"
    socks_debug: ""
    socks_bind_ipv6_enabled: false
    socks_bind_ipv6: "::"
    socks_log_folder: /var/log/danted
    socks_pid_folder: /var/run/danted
    socks_logrotate_days: 14
    socks_config: /etc/danted.conf
    socks_workers: 4
    socks_html_output: true
    socks_access_rules: {}
    #socks_access_rules:
    #  - name: "Description"
    #    log: "" <- empty to disable log
    #    src:
    #      - 10.62.0.162
    #      - 10.62.0.141
    #    dst:
    #      - 173.249.21.224/32
    #      - onkeldom.eu
    #
    # Caddyserver default settings
    #
    caddy_enabled: true
    caddy_group: www-data
    caddy_user: www-data
    caddy_logrotate_days: 14
    caddy_web_path: /var/www
    caddy_log_folder: /var/log/caddy
    # Define basic auth for files
    caddy_basic_auth: true
    caddy_basic_auth_user: proxy
    caddy_basic_auth_pass: "JDJhJDE0JHI5Wlpua1BsQkF6M3o2TkpzclNmOU9JNHNabWY5V3ZkZHpkeEpIUWdaRFV2NDNyQS9oR3Zx" # pw: proxy | generate pass with caddy hash-password
    caddy_basic_auth_paths: "/socks.html /squid.html /squid_acls /squidguard"
    # Define caddy pac-access forbidden ip lists
    caddy_forbidden_ips_text: "IP-Address blocked"
    caddy_forbidden_ips_enable: true
    caddy_forbidden_ips: ""
    # Define caddy pac-access allowed ip lists
    caddy_allowed_ips_text: "IP-Address not defined as allowed"
    caddy_allowed_ips_enable: true
    caddy_allowed_ips: "10.0.0.0/8 192.168.0.0/16 169.254.0.0/16"
    #
    # PAC-File default settings
    #
    pac_enabled: true
    pac_file_proxys:
      - name: proxy
        address: "{{ ansible_hostname }}.{{ ansible_domain }}"
    pac_file_rules:
      # Go direct for internal and special partner sites
      - name: '\"*.{{ ansible_domain }}\"'
        type: "shExpMatch"
        return: direct
      # Go direct for defines networks
      - name: '\"169.254.0.0\", \"255.255.0.0\"'
        type: "isInNet"
        return: direct
      - name: '\"172.16.0.0\", \"255.240.0.0\"'
        type: "isInNet"
        return: direct
      - name: '\"192.168.0.0\", \"255.255.0.0\"'
        type: "isInNet"
        return: direct
      - name: '\"10.0.0.0\", \"255.0.0.0\"'
        type: "isInNet"
        return: direct
      - name: '\"100.64.0.0\", \"255.192.0.0\"'
        type: "isInNet"
        return: direct
      - name: '\"fe80:*\"'
        type: "shExpMatch"
        return: direct
      - name: '\"fc00:*\"'
        type: "shExpMatch"
        return: direct
    #
    # Squid default settings
    #
    squid_enabled: true
    squid_html_output: true
    squid_user: proxy
    squid_group: proxy
    squid_logrotate_days: 14
    squid_log_folder: /var/log/squid
    squid_pid_folder: /var/run/squid
    squid_config_dir: /etc/squid
    squid_port: 3128
    # Define Squid Logformat
    squid_logformat_name: squid_json
    squid_logformat: '{"proxy_squid_ip":"%la","proxy_squid_fqdn":"{{ansible_hostname }}.{{ansible_domain}}","proxy_client_ip":"%>a","proxy_client_fqdn":"%>A","proxy_user_agent":"%{User-Agent}>h","proxy_timestamp":"%tl","proxy_short_message":"%rm %ru HTTP/%rv","proxy_dst_host":"%{Host}>h","proxy_dst_ip":"%<a","proxy_dst_url":"%ru","proxy_http_status":"%>Hs","proxy_http_method":"%rm","proxy_http_referer":"%{Referer}>h","proxy_mime_content_type":"%mt","proxy_response_time":"%tr","proxy_request_size":"%>st","proxy_reply_size":"%<st","proxy_squid_request_status":"%Ss","proxy_squid_hierarchy_status":"%Sh"}'
    squid_url_rewrite_programm: "/usr/bin/squidGuard -c {{ squid_config_dir }}/{{ squidguard_config_file }}"
    squid_url_rewrite_childen: "25 startup=10 idle=10 concurrency=0"
    squid_config_custom:
      visible_hostname: "{{ ansible_hostname }}.{{ ansible_domain }}"
      cache_mgr: "hostmaster@{{ ansible_domain }}"
      maximum_object_size_in_memory: 512 KB
      maximum_object_size: 4096 KB
      client_persistent_connections: "on"
      server_persistent_connections: "on"
      forwarded_for: delete
      via: "on"
      acl_uses_indirect_client: "on"
      delay_pool_uses_indirect_client: "on"
      log_uses_indirect_client: "on"
      cache_mem: 512 MB
      cache_store_log: /var/log/squid/store.log
      cache_log: /var/log/squid/cache.log
      client_db: "on"
      collapsed_forwarding: "on"
      detect_broken_pconn: "on"
      dns_defnames: "on"
      dns_retransmit_interval: 2 seconds
      dns_timeout: 5 minutes
      half_closed_clients: "off"
      httpd_suppress_version_string: "on"
      ignore_unknown_nameservers: "on"
      pipeline_prefetch: "on"
      retry_on_error: "off"
      strip_query_terms: "off"
      uri_whitespace: strip
      icp_access: deny all
      http_reply_access: allow all
      cache: deny all
      ident_lookup_access: deny all
      log_mime_hdrs: "on"
      logfile_rotate: 0
      ipcache_size: 10240
      max_filedesc: 16384
      forward_timeout: 200 seconds
      connect_timeout: 30 seconds
      read_timeout: 200 seconds
      request_timeout: 200 seconds
      persistent_request_timeout: 1 minute
      client_lifetime: 4 hours
      coredump_dir: /var/spool/squid
    squid_config_refresh_pattern:
      - ".jpg 14400 50% 18000 override-expire override-lastmod reload-into-ims ignore-reload ignore-no-cache ignore-private ignore-auth"
      - "-i \\.(gif|png|jpg|jpeg|ico|bmp)$ 14400 50% 18000 override-expire override-lastmod reload-into-ims ignore-reload ignore-no-cache ignore-private ignore-auth"
      - "-i \\.(iso|avi|wav|mp3|mp4|mpeg|swf|flv|x-flv|mpg|wma|ogg|wmv|asx|asf)$ 14400 50% 18000 override-expire override-lastmod reload-into-ims ignore-reload ignore-no-cache ignore-private ignore-auth"
      - "-i \\.(cab|exe|ms[i|u|f]|asf|wm[v|a]|dat|zip) 4320 80% 43200 reload-into-ims"
      - "^ftp:              1440    20%    10080"
      - "^gopher:           1440     0%     1440"
      - "-i (/cgi-bin/|\\?)    0     0%        0"
      - ".                     0    20%     4320"
    squid_ssl_ports:
      - 443
    squid_safe_ports:
      - 80
      - 443
    squid_src_acls:
      - name: clients
        comment: Clients
        source: |
          # File managed by Ansible
          10.0.0.0/8
          192.168.0.0/16
          169.254.0.0/16
      - name: admins
        comment: Administrators
        source: |
          # File managed by Ansible
          10.10.10.10
    squid_dst_acls:
      - name: allow_admins
        comment: Allow Admins free Internet access
        acess: allow
        source: admins
      - name: whitelist
        comment: Allow Clients to acces domains from whitelist stored in files/squid/acl_dst_whielist.lst
        type: dstdomain
        access: allow
        file: whitelist # acl_dst and .lst gets automatic in tasks
        source: clients
      - name: deny_clients
        comment: Deny all other clients
        access: deny # ignores squidguard config
        source: clients
    #squid_dst_acls: # exmaple 1
    #  - name: limit_rate_monitoring
    #    comment: Monitoring Rate Limiting
    #    type: maxconn
    #    access: deny
    #    source: monitoring
    #    content: 15
    #  # Allow to ips and domains
    #  - name: whitelist_monitoring_ips
    #    comment: Monitoring Destination IPs
    #    type: dst
    #    access: allow
    #    source: monitoring
    #    file: whitelist_monitoring_ips
    #  - name: whitelist_monitoring_domains
    #    comment: Monitoring Destination Domains
    #    type: dstdomain
    #    access: allow
    #    source: monitoring
    #    file: whitelist_monitoring_domains
    #  # Deny all Other
    #  - name: deny_monitoring
    #    comment: Monitoring Deny all other
    #    access: deny
    #    source: monitoring
    #    deny_info: monitoring_access_denied
    #squid_dst_acls: # exmaple 2
    #  - name: blacklist
    #    comment: Blacklist
    #    access: deny
    #    type: dstdomain
    #    deny_info: access_blocked # Define Squid deny_info pages defined in squid_template_errors above
    #    source: clients
    ### With destination file
    #    file: blacklist (filename: acl_dst_blacklist.lst)
    #  - name: whitelist
    #    comment:  Internal Domains
    #    access: allow
    #    type: dstdomain
    #    source: clients
    ### With destination file
    #    file: whitelist (filename: acl_dst_whitelist.lst)
    ### OR with destination definition
    #    destination: |
    #      .github.com
    #      .onkeldom.eu
    #      .cloudflare.com
    #      api.cloudflare.net
    #  - name: whitelist_networks
    #    comment: Internal Domains
    #    access: allow
    #    type: dst
    #    source: clients
    ### With destination file
    #    file: whitelist_networks (filename: acl_dst_whitelist_networks.lst)
    ### OR with destination definition
    #    destination: |
    #      100.64.0.0/10
    #
    # SquidGuard default settings
    #
    squidguard_enabled: true
    squidguard_html_output: true
    squidguard_log_folder: /var/log/squidguard
    squidguard_script_dir: /usr/local/bin/
    squidguard_redirect_url: "http://{{ ansible_hostname }}.{{ ansible_domain }}/cgi-bin/squidguard.cgi?clientaddr=%a&clientname=%n&clientuser=%i&srcclass=%s&targetclass=%t&url=%u"
    squidguard_config_file: squidguard.conf
    squidguard_dbhome: "{{ squid_config_dir }}/guard.d/blacklists"
    squidguard_web_allow_all: true
    squidguard_blacklist_url: "ftp://ftp.univ-tlse1.fr/pub/reseau/cache/squidguard_contrib/blacklists.tar.gz"
    # alternative list:       "ftp://ftp.ut-capitole.fr/pub/reseau/cache/squidguard_contrib/blacklists.tar.gz"
    # Sort List from allow -> deny
    squidguard_blacklist:
      ##### DVAG files
      - name: whitelist
        log: true
        redirect_url: ""
        access: allow # deny/allow
        file: whitelist # store in ansible-role-squid4/files/proxy_{{ ansible_proxy }}/squidguard_{{ file }}.lst
        type:
          - domainlist
      - name: blacklist
        log: true
        redirect_url: ""
        access: deny # deny/allow
        file: blacklist # store in ansible-role-squid4/files/proxy_{{ ansible_proxy }}/squidguard_{{ file }}.lst
        type:
          - domainlist
      ##### whitelist categories
      - name: bank
        log: true
        access: allow # deny/allow
        type:
          - domainlist
      - name: financial
        log: true
        access: allow # deny/allow
        type:
          - domainlist
          - urllist
      ##### blacklist categories
      - name: adult
        log: true
        redirect_url: ""
        access: deny # deny/allow
        type:
          - domainlist
          - urllist
          - expressionlist
      - name: aggressive
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: agressif
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: ddos
        log: true
        access: deny
        type:
          - domainlist
      - name: drugs
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: gambling
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: hacking
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: malware
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: phishing
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: sexual_education
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: porn
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: vpn
        log: true
        access: deny
        type:
          - domainlist
      - name: violence
        log: true
        access: deny
        type:
          - domainlist
          - urllist
      - name: warez
        log: true
        access: deny
        type:
          - domainlist
          - urllist
    #
    # Squid define errors page
    #
    # Define squid custom templates
    squid_template: false
    squid_template_file: squid.errors.client.html.j2
    squid_template_errors:
      - name: access_denied
        title_line: "Fehler: Webseiten Zugriff verweigert"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Webseiten Zugriff verweigert"
        content_header_line: "Die Sicherheitsüberprüfung dieser Webseite ist noch nicht erfolgt."
        content_html: |
          <p>Der Zugriff auf diese Seite wurde verwehrt.</p>
      - name: acl_time_quota_exceeded
        title_line: "Fehler: Zeitguthaben aufgebraucht"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Zeitguthaben aufgebraucht"
        content_header_line: ""
        content_html: |
          <p>Ihr Online-Zeitguthaben ist nun aufgebraucht. Es wird automatisch erneuert, sobald der nächste vereinbarte Zyklus beginnt.<br></p>
      - name: agent_configure
        title_line: "Fehler: Webbrowserkonfiguration"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Webbrowserkonfiguration"
        content_header_line: "Ihre Webbrowserkonfiguration muss korrigiert werden um dieses Netzwerk zu nutzen."
        content_html: |
          <p>Die Konfiguration Ihres Webbrowsers scheint fehlerhaft zu sein.<br>Wenden Sie sich bitte an die Innendiensthotline (-500).</p>
      - name: agent_wpad
        title_line: "Fehler: Webbrowserkonfiguration"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Webbrowserkonfiguration"
        content_header_line: "Ihre Webbrowserkonfiguration muss korrigiert werden um dieses Netzwerk zu nutzen."
        content_html: |
          <p>Die Konfiguration Ihres Webbrowsers scheint fehlerhaft zu sein.<br>Wenden Sie sich bitte an die Innendiensthotline (-500).</p>
      - name: cache_access_denied
        title_line: "Fehler: Webseiten Cache Zugriff verweigert"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Webseiten Zugriff verweigert"
        content_header_line: "Die Sicherheitsüberprüfung dieser Cache Webseite ist noch nicht erfolgt."
        content_html: |
          <p>Benötigen Sie diese Seite für Ihre Tätigkeit? Dann können Sie uns diese melden und freischalten lassen. </br> Klicken Sie dazu <a href="mailto:ticketanlieferungscc@dvag.com?subject=Proxy_Whitelisting%20-%20%U&amp;body=URL:%20%U%0ADomain:%20%H%0APort:%20%p%0AClientIP:%20%i%0ATimestamp:%20%t%0A%0AFreischaltungsgrund:%20%23BITTE%20GRUND%20ANGEBEN%0A%0A%0A%0ADebuginfo:%0A%R">hier</a> und senden uns eine E-Mail.</p>
          <p></br></p>
          <p>Bitte geben Sie den Grund der Freischaltung an und versenden Sie die automatisch generierte E-Mail, ohne weitere Veränderungen vorzunehmen.</p>
          <p></br></p>
          <p>Gemeldete Seiten werden schnellstmöglich geprüft und freigegeben.</p>
          <p></br/></p>
          <p>Vielen Dank für Ihre Unterstützung.</p>
      - name: cache_mgr_access_denied
        title_line: "Fehler: Webseiten Authentifizierungs Zugriff verweigert"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Webseiten Zugriff verweigert - Authentifizierung"
        content_header_line: "Die Anmeldung am Proxyserver konnte nicht verifiziert werden."
        content_html: |
          <p>Sie sind momentan nicht berechtigt %U von diesem Proxyserver abzurufen, bis Sie sich authentifiziert haben.<br></p>
      - name: cannot_forward
        title_line: "Fehler: Die angeforderte URL konnte nicht gefunden werden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Die angeforderte URL konnte nicht gefunden werden<"
        content_header_line: "Die Anfrage kann nicht weitergeleitet werden"
        content_html: |
          <p>Ihre Anfrage kann an den Folgeserver nicht weitergeleitet werden.<br></p>
      - name: conflict_host
        title_line: "Fehler: Die angeforderte URL konnte nicht gefunden werden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Die angeforderte URL konnte nicht gefunden werden"
        content_header_line: "Die Seite, die Sie aufrufen möchte, konnte nicht gefunden werden."
        content_html: |
          <p>Es ist möglich, dass Sie sich bei der Eingabe der Seite verschrieben haben, oder die Webseite umgezogen bzw. gelöscht wurde.<br></p>
      - name: connect_fail
        title_line: "Fehler: Verbindung Fehlgeschlagen"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Verbindung Fehlgeschlagen"
        content_header_line: "Verbindung zu %I ist Fehlgeschlagen."
        content_html: |
          <p>Der Zielhost oder das Zielnetzwerk ist momentan nicht verfügbar. Bitte wiederholen sie die Anfrage.<br></p>
      - name: dir_listing
        title_line: "Verzeichnis: %U"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: ""
        content_header_line: "Verzeichnis Auflistung"
        content_html: |
          <table id="dirlisting" summary="Verzeichnis Auflistung">
          <tr>
          <th><a href="../"><img border="0" src="/squid-internal-static/icons/silk/arrow_up.png" alt=""></a></th>
          <th nowrap="nowrap"><a href="../">Übergeordnetes Verzeichnis</a> (<a href="/">Stammverzeichnis</a>)</th>
          </tr>
          %g
          </table>
      - name: dns_fail
        title_line: "Fehler: Die angeforderte URL konnte nicht gefunden werden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Die angeforderte URL konnte nicht gefunden werden"
        content_header_line: "Der DNS-Server meldete:"
        content_html: |
          <p><code>%z</code><br></p>
          <p>Das heißt, dass der Proxyserver nicht in der Lage war den Hostnamen aufzulösen der in der URL gefunden wurde. Überprüfen sie ob die Adresse korrekt ist.<br></p>
      - name: esi
        title_line: "Fehler: Die angeforderte URL konnte nicht gefunden werden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "ESI-Verarbeitung fehlgeschlagen."
        content_header_line: "Der ESI-Prozessor meldete:"
        content_html: |
          <p><code>%Z</code><br></p>
          <p>Das heißt, dass der Ersatz nicht in der Lage war das ESI Template zu verarbeiten. Bitte melden sie diesen Fehler dem Webmaster.<br></p>
      - name: forwarding_denied
        title_line: "Fehler: Weiterleitung verweigert"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Weiterleitung verweigert"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Dieser Proxyserver wird ihre Anfrage nicht weiterleiten, da er versucht ein Geschwisterverhältnis zu erzwingen. Wahrscheinlich ist der Client auf %i ein Proxyserver der falsch konfiguriert wurde.<br></p>
      - name: ftp_disabled
        title_line: "Fehler: FTP deaktiviert"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP deaktiviert"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>FTP ist deaktiviert<br></p>
          <p>Dieser Proxyserver unterstützt kein FTP.<br></p>
      - name: ftp_failure
        title_line: "Fehler: FTP Protokollfehler"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP Protkollfehler"
        content_header_line: "Ein FTP Protokollfehler ist bei der URL <a href=\"%U\">%U</a> aufgetreten."
        content_html: |
          <p>Squid sendete das folgende FTP Kommando:<br></p>
          <p><code>%f</code><br></p>
          <p>Der Server antwortete:<br></p>
          <p><code>%F</code><br></p>
          <p><code>%g</code><br></p>
      - name: ftp_forbidden
        title_line: "Fehler: FTP Authentifizierung fehlgeschlagen"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP Authentifizierung fehlgeschlagen"
        content_header_line: "Die FTP Authentifizierung bei der URL <a href=\"%U\">%U</a> ist Fehlgeschlagen."
        content_html: |
          <p>Squid sendete das folgende FTP Kommando:<br></p>
          <p><code>%f</code><br></p>
          <p>Der Server antwortete:<br></p>
          <p><code>%F</code><br></p>
          <p><code>%g</code><br></p>
      - name: ftp_not_found
        title_line: "Fehler: FTP URL nicht gefunden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP URL nicht gefunden"
        content_header_line: "Die folgende URL konnte nicht gefunden werden: <a href=\"%U\">%U</a>"
        content_html: |
          <p>Squid sendete das folgende FTP Kommando:<br></p>
          <p><code>%f</code><br></p>
          <p>Der Server antwortete:<br></p>
          <p><code>%F</code><br></p>
          <p><code>%g</code><br></p>
          <p>Die Ursache kann eine FTP URL mit einem absoluten Pfad sein (was nicht RFC 1738 konform ist). Wenn dies der Fall ist, ist die Datei unter <a href="%B">%B</a> zu finden.<br></p>
      - name: ftp_put_created
        title_line: "Fehler: FTP PUT Erfolgreich"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP PUT Erfolgreich"
        content_header_line: "Operation erfolgreich"
        content_html: |
          <p>Datei erstellt.<br></p>
      - name: ftp_put_error
        title_line: "Fehler: FTP Upload fehlgeschlagen"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP Upload fehlgeschlagen"
        content_header_line: "Ein FTP Protokollfehler ist bei der URL <a href=\"%U\">%U</a> aufgetreten."
        content_html: |
          <p><br></p>
          <p>Squid sendete das folgende FTP Kommando:<br></p>
          <p><code>%f</code><br></p>
          <p>Der Server antwortete:<br></p>
          <p><code>%F</code><br></p>
          <p>Das heißt, dass der FTP Server keine Berechtigung oder nicht genug Plattenplatz zum Speichern der Datei zur Verfügung hat. Überprüfen sie Pfad, Berechtigungen und Plattenplatz und wiederholen Sie die Anfrage.<br></p>
      - name: ftp_put_modified
        title_line: "Fehler: FTP PUT Erfolgreich"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "FTP PUT Erfolgreich"
        content_header_line: "Operation erfolgreich"
        content_html: |
          <p>Datei aktualisiert.<br></p>
      - name: ftp_unanvailable
        title_line: "Fehler: URL konnte nicht gefunden werden"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "URL konnte nicht gefunden werden"
        content_header_line: "Der FTP Server war zu beschäftigt um die URL: <a href=\"%U\">%U</a> abzurufen"
        content_html: |
          <p>Squid sendete das folgende FTP Kommando:<br></p>
          <p><code>%f</code><br></p>
          <p>Der Server antwortete:<br></p>
          <p><code>%F</code><br></p>
          <p><code>%g</code><br></p>
      - name: gateway_failure
        title_line: "Fehler: Gateway Proxy Fehler"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Gateway Proxy Fehler"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Ein nicht-behebbarer interner Fehler oder ein Konfigurationsproblem verhindert die Ausführung der Anfrage.<br></p>
      - name: icap_failure
        title_line: "Fehler: ICAP Protokoll fehler"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "ICAP Protokoll fehler"
        content_header_line: "Das heißt, dass etwas mit der ICAP Kommunikation nicht stimmt."
        content_html: |
          <p>Der ICAP Server ist nicht erreichbar.<br></p>
          <p>Die Antwort des ICAP Servers war ungültig.<br></p>
      - name: invalid_req
        title_line: "Fehler: Ungültige Anfrage"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Ungültige Anfrage"
        content_header_line: "<b>Ungültige Anfrage</b> Fehler erhalten als versucht wurde die Anfrage zu bearbeiten:"
        content_html: |
          <p>Mögliche Probleme sind:<br>
          <ul>
          <li id="missing-method"><p>Fehlende oder unbekannte Anfragemethode.</p></li>
          <li id="missing-url"><p>Fehlende URL.</p></li>
          <li id="missing-protocol"><p>Fehlende HTTP-Version (HTTP/1.0).</p></li>
          <li><p>Anfrage ist zu lang.</p></li>
          <li><p>Content-Length fehlt für POST oder PUT Anfragen.</p></li>
          <li><p>Ungültiges Zeichen im Hostname; Unterstriche sind nicht erlaubt.</p></li>
          <li><p>HTTP/1.1 <q>Expect</q> wird von einer HTTP/1.0 Software erfragt</p></li>
          </ul>
          <br>
          </p>
          <script language=\"javascript\">
            if (\'%M\' != \'[unknown method]\') document.getElementById(\'missing-method\').style.display = \'none\';
            if (\'%u\' != \'[no URL]\') document.getElementById(\'missing-url\').style.display = \'none\';
            if (\'%P\' != \'[unknown protocol]\') document.getElementById(\'missing-protocol\').style.display = \'none\';
          </script>
      - name: invalid_resp
        title_line: "Fehler: Ungültige Antwort"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Ungültige Antwort"
        content_header_line: "<b>Ungültige Antwort</b> Fehler erhalten als versucht wurde die Anfrage zu bearbeiten:"
        content_html: |
          <p>Die HTTP Antwortnachricht, die vom Kontaktierten Server empfangen wurde, wurde nicht verstanden oder ist falsch. Bitte kontaktieren sie den Webmaster.<br></p>
          <p>Ihr Cache Administrator ist in der Lage ihnen mehr über das Problem zu erklären, falls dies Notwendig ist.<br></p>
      - name: invalid_url
        title_line: "Fehler: Syntax Fehler"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Ungültige URL"
        content_header_line: "Der Syntax der angeforderten URL ist falsch."
        content_html: |
          <p>Mögliche Probleme sind:<br>
          <ul>
          <li><p>Fehlendes oder ungültiges Adressprotokoll (Versuchen sie zum Beispiel<q>http://</q>)</p></li>
          <li><p>Fehlender Hostname</p></li>
          <li><p>Ungültiger Doppel-Escape im URL-Pfad</p></li>
          <li><p>Ungültiges Zeichen im Hostname; Unterstriche sind nicht erlaubt.</p></li>
          </ul>
          <br>
          <p>
      - name: lifetime_exp
        title_line: "Fehler: Zeitüberschreitung"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Zeitüberschreitung"
        content_header_line: "Zeitlimit der Verbindung erreicht."
        content_html: |
          <p>Squid hat die Anfrage beendet, da die maximale Verbindungszeit überschritten wurde.<br></p>
      - name: no_relay
        title_line: "Fehler: Kein Wais Relay"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Kein Wais Relay"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Es ist kein WAIS Relay für diesen Proxyserver definiert! Sagen sie dies dem Administrator.<br></p>
      - name: only_if_cached_miss
        title_line: "Fehler: Cache missed"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Cached missed"
        content_header_line: "Kein gültiges Dokument wurde im Cache gefunden und <q>only-if-cached</q> Option wurde angegeben."
        content_html: |
          <p>Sie haben eine Anfrage mit der <q>only-if-cached</q> Cache Kontrolloption getätigt. Das Dokument wurde nicht im Cache gefunden, <em>oder</em> es forderte eine Aktualisierung an welche durch die <q>only-if-cached</q> Option unterbunden wurde.<br></p>
      - name: precondition_failed
        title_line: "Fehler: Bedingung nicht erfüllt"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Bedingung nicht erfüllt"
        content_header_line: "Dies Bedeutet:"
        content_html: |
          <p>Mindestens eine Bedingung, die vom HTTP Client vorrausgesetzt wird, wurde nicht erfüllt.<br></p>
      - name: read_error
        title_line: "Fehler: Lesefehler"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Lesefehler"
        content_header_line: "Das System antwortete:"
        content_html: |
          <p>Ein Fehler ist beim Lesen vom Netzwerk aufgetreten. Bitte wiederholen sie die Anfrage.<br></p>
      - name: read_timeout
        title_line: "Fehler: Zeitüberschreitung beim warten"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Zeitüberschreitung beim warten"
        content_header_line: "Das System antwortete: <i>%E</i>"
        content_html: |
          <p>Zeitüberschreitung beim Warten auf Daten des Netzwerks. Das Netzwerk oder der Server könnte nicht verfügbar oder überlastet sein. Bitte versuchen sie es erneut.<br></p>
      - name: secure_connect_fail
        title_line: "Fehler: Keine sichere Verbindung"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Keine sichere Verbindung"
        content_header_line: "Konnte keine sichere Verbindung zu %I herstellen"
        content_html: |
          <p><code>%E (TLS code: %x)</code></p>
          <p><code>%D</code><br></p>
          <p>Dieser Proxy und der Zielhost waren nicht in der Lage Sicherheitseinstellungen auszuhandeln die beidseitig akzeptiert werden. Es ist möglich dass der Zielhost keine sicheren Verbindungen unterstützt oder der Proxy nicht mit dem Sicherheitszertifikat des Hosts einverstanden ist.<br></p>
      - name: shutting_down
        title_line: "Fehler: System herunterfahren"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "System herunterfahren"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Dieser Proxyserver wird momentan heruntergefahren und kann daher die Anfrage nicht bearbeiten. Bitte wiederholen sie die Anfrage gleich noch einmal.<br></p>
      - name: socket_failure
        title_line: "Fehler: Keine freien verbindungen"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Keine freien Verbindungen"
        content_header_line: "Das System antwortete: <i>%E</i>"
        content_html: |
          <p>Squid kann keinen TCP-Socket erstellen, wahrscheinlich aufgrund von großer Systemlast. Bitte wiederholen Sie die Anfrage.<br></p>
      - name: too_big
        title_line: "Fehler: Anfrage oder Antwort zu lang"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Inhalt zu groß"
        content_header_line: "Die Anfrage oder Antwort ist zu lang."
        content_html: |
          <p>Für einen POST-Request ist die hochzuladene Resource zu groß.<br></p>
          <p>Für einen GET-Request ist die angeforderte Resource zu groß.<br></p>
          <p>Diese Einschränkungen wurden vom den Administratoren eingerichtet die diesen Proxyserver betreiben. Bitte kontaktieren Sie ihn, falls Sie denken, dass dies ein Fehler ist.<br></p>
      - name: unsup_httpversion
        title_line: "Fehler: Nicht unterstützte HTTP-Version"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Nicht unterstützte HTTP-Version"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Dieser Squid akzeptiert die angeforderte HTTP Version nicht.<br></p>
      - name: unsup_req
        title_line: "Fehler: Anfragemethode nicht unterstützt"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Anfragemethode nicht unterstützt"
        content_header_line: "Anfragemethode und Protokoll nicht unterstützt"
        content_html: |
          <p>Squid unterstützt nicht alle Anfragemethoden für alle Protokolle. Sie können zum Beispiel keine POST Anfrage über das Gopher Protokoll senden.<br></p>
      - name: urn_resolve
        title_line: "Fehler: URN nicht auflösbar"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "URN nicht auflösbar"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URN <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Hey, erwarten sie nicht zuviel von URNs auf %T :)<br></p>
      - name: write_error
        title_line: "Fehler: Fehler beim schreiben"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Fehler beim schreiben"
        content_header_line: "Das System antwortete: <i>%E</i>"
        content_html: |
          <p>Ein Fehler ist beim Schreiben auf das Netzwerk aufgetreten. Bitte wiederholen sie die Anfrage.<br></p>
      - name: zero_size_object
        title_line: "Fehler: Nullgrößenantwort"
        footer_line: "&copy; | Kontakt: <a href=\"mailto:%w\"> %w</a>"
        header_line: "Nullgrößenantwort"
        content_header_line: "Der folgende Fehler wurde beim Versuch die URL <a href=\"%U\">%U</a> zu holen festgestellt:"
        content_html: |
          <p>Squid hat keine Daten für diese Anfrage empfangen.<br></p>
```

### Playbook

```yaml
---
- hosts: all
  roles:
  - ansible-role-proxy
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
