---
published: true
---
## Алгоритм действий, если нужно дебажить cli скрипт удаленно

1. Установить xdebug на **удаленной** машине.
2. Далее настроить конфиг xdebug:
```
zend_extension=xdebug.so
xdebug.remote_handler="dbgp"
xdebug.remote_port=8888
xdebug.remote_host=localhost
xdebug.remote_autostart = on
xdebug.remote_start = on
xdebug.remote_enable = 1
xdebug.idekey="PHPSTORM"
xdebug.profiler_enable=0
xdebug.profiler_enable_trigger=1
xdebug.profiler_enable_trigger_value="xdebug-profile"
xdebug.profiler_output_name="cachegrind.out.%H"
xdebug.remote_log="/var/log/xdebug.log"
```

```
xdebug support => enabled
xdebug.auto_trace => Off => Off
xdebug.cli_color => 0 => 0
xdebug.collect_assignments => Off => Off
xdebug.collect_includes => On => On
xdebug.collect_params => 0 => 0
xdebug.collect_return => Off => Off
xdebug.collect_vars => Off => Off
xdebug.coverage_enable => On => On
xdebug.default_enable => On => On
xdebug.dump.COOKIE => no value => no value
xdebug.dump.ENV => no value => no value
xdebug.dump.FILES => no value => no value
xdebug.dump.GET => no value => no value
xdebug.dump.POST => no value => no value
xdebug.dump.REQUEST => no value => no value
xdebug.dump.SERVER => no value => no value
xdebug.dump.SESSION => no value => no value
xdebug.dump_globals => On => On
xdebug.dump_once => On => On
xdebug.dump_undefined => Off => Off
xdebug.extended_info => On => On
xdebug.file_link_format => no value => no value
xdebug.filename_format => no value => no value
xdebug.force_display_errors => Off => Off
xdebug.force_error_reporting => 0 => 0
xdebug.gc_stats_enable => Off => Off
xdebug.gc_stats_output_dir => /tmp => /tmp
xdebug.gc_stats_output_name => gcstats.%p => gcstats.%p
xdebug.halt_level => 0 => 0
xdebug.idekey => PHPSTORM => PHPSTORM
xdebug.max_nesting_level => 256 => 256
xdebug.max_stack_frames => -1 => -1
xdebug.overload_var_dump => 2 => 2
xdebug.profiler_aggregate => Off => Off
xdebug.profiler_append => Off => Off
xdebug.profiler_enable => Off => Off
xdebug.profiler_enable_trigger => On => On
xdebug.profiler_enable_trigger_value => xdebug-profile => xdebug-profile
xdebug.profiler_output_dir => /tmp => /tmp
xdebug.profiler_output_name => cachegrind.out.%H => cachegrind.out.%H
xdebug.remote_addr_header => no value => no value
xdebug.remote_autostart => Off => Off
xdebug.remote_connect_back => Off => Off
xdebug.remote_cookie_expire_time => 3600 => 3600
xdebug.remote_enable => On => On
xdebug.remote_handler => dbgp => dbgp
xdebug.remote_host => localhost => localhost
xdebug.remote_log => /var/log/xdebug.log => /var/log/xdebug.log
xdebug.remote_mode => req => req
xdebug.remote_port => 8888 => 8888
xdebug.remote_timeout => 200 => 200
xdebug.scream => Off => Off
xdebug.show_error_trace => Off => Off
xdebug.show_exception_trace => Off => Off
xdebug.show_local_vars => Off => Off
xdebug.show_mem_delta => Off => Off
xdebug.trace_enable_trigger => Off => Off
xdebug.trace_enable_trigger_value => no value => no value
xdebug.trace_format => 0 => 0
xdebug.trace_options => 0 => 0
xdebug.trace_output_dir => /tmp => /tmp
xdebug.trace_output_name => trace.%c => trace.%c
xdebug.var_display_max_children => 128 => 128
xdebug.var_display_max_data => 512 => 512
xdebug.var_display_max_depth => 3 => 3
```
3. Далее перезагрузить php-fpm
4. Далее настроить phpstorm: Settings->Languages & Frameworks->PHP->Debug![Screenshot from 2018-11-15 17-06-21.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-06-21.png)
![Screenshot from 2018-11-15 17-06-15.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-06-15.png) ![Screenshot from 2018-11-15 17-06-11.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-06-11.png) ![Screenshot from 2018-11-15 17-05-55.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-05-55.png) ![Screenshot from 2018-11-15 17-05-38.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-05-38.png)
 ![Screenshot from 2018-11-15 17-05-30.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-05-30.png) ![Screenshot from 2018-11-15 17-05-21.png]({{site.baseurl}}/images/Screenshot from 2018-11-15 17-05-21.png)




