riak_core_app.erl

  1.riak_core_util:start_app_deps(riak_core).
  2.RingStateDir = app_helper:get_env(riak_core, ring_state_dir),
  3.cluster_info:register_app(riak_core_cinfo_core).
  4.riak_core_bucket:append_bucket_defaults(riak_core_bucket_type:defaults()).
  5.case riak_core_sup:start_link() of
      {ok, Pid} ->
        riak_core:register(riak_core, [{stat_mod, riak_core_stat},
                                      {permissions, [get_bucket,
                                                      set_bucket,
                                                      get_bucket_type,
                                                      set_bucket_type]}]),
      ok = riak_core_ring_events:add_guarded_handler(riak_core_ring_handler,[]),
      riak_core_capability:register({riak_core, vnode_routing},
                                    [proxy, legacy],
                                    legacy,
                                    {riak_core,
                                      legacy_vnode_routing,
                                      [{true, legacy}, {false, proxy}]}),
      riak_core_capability:register({riak_core,staged_joins},
                                    [true, false],
                                    false),
      riak_core_capability:register({riak_core, resizable_ring},
                                    [true, false],
                                    false),
      riak_core_capability:register({riak_core, fold_req_version},
                                    [v2, v1],
                                    v1),
      riak_core_capability:register({riak_core, security},
                                    [true, false],
                                    false),
      riak_core_capability:register({riak_core, bucket_type},
                                    [true, false],
                                    false),
      riak_core_capability:register({riak_core, net_ticktime},
                                    [true, false],
                                    false),
      riak_core_cli_registry:load_schema(),
      riak_core_cli_registry:register_node_finder(),
      riak_core_cli_registry:register_cli(),
      
      {ok, Pid};
    {error, Reason} ->
      {error, Reason}
  end.
  
  
