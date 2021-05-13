---
layout: post
title: (TIL) Print Duct's Config EDN in Repl
---
We can access duct's config edn can be accessed through `config` variable in REPL.
It includes whole map, not only what is written inside config.edn file's.

~~~ clojure
dev=> (pprint config)
{:duct.handler.static/method-not-allowed {:headers {"Content-Type" "text/html; charset=UTF-8"},
                                          :body #duct/resource "duct/module/web/errors/405.html"},
 :duct.logger/timbre {:level :debug,
                      :appenders {:duct.logger.timbre/spit #ig/ref :duct.logger.timbre/spit,
                                  :duct.logger.timbre/brief #ig/ref :duct.logger.timbre/brief}},
 :duct.logger.timbre/brief {:min-level :report},
 :duct.router/reitit {:routes [["/"
                                ["inventory"
                                 {:handler #ig/ref :smallshop.handler/inventory,
                                  :middleware [#ig/ref :smallshop.middleware/common]}]
                                [""
                                 {:handler #ig/ref :smallshop.handler/welcome,
                                  :middleware [#ig/ref :smallshop.middleware/common]}]]],
                      :reitit.ring/opts {:data {:coercion #object[reitit.coercion.spec$create$reify__17820
                                                                  "0x41a3816c"
                                                                  "reitit.coercion.spec$create$reify__17820@41a3816c"],
                                                :middleware [{:name :reitit.ring.coercion/coerce-exceptions,
                                                              :compile #object[reitit.ring.coercion$fn__15817
                                                                               "0x5cb434b3"
                                                                               "reitit.ring.coercion$fn__15817@5cb434b3"]}
                                                             {:name :reitit.ring.coercion/coerce-request,
                                                              :spec :reitit.spec/parameters,
                                                              :compile #object[reitit.ring.coercion$fn__15794
                                                                               "0x6b6a330b"
                                                                               "reitit.ring.coercion$fn__15794@6b6a330b"]}
                                                             {:name :reitit.ring.coercion/coerce-response,
                                                              :spec :reitit.spec/responses,
                                                              :compile #object[reitit.ring.coercion$fn__15804
                                                                               "0x35699a8b"
                                                                               "reitit.ring.coercion$fn__15804@35699a8b"]}]}},
                      :reitit.ring/handlers nil,
                      :reitit.ring/default-handlers {:not-found #ig/ref :duct.handler.static/not-found,
                                                     :not-acceptable #ig/ref :duct.handler.static/bad-request,
                                                     :method-not-allowed #ig/ref :duct.handler.static/method-not-allowed}},
 :duct.middleware.web/format {},
 :duct.middleware.web/log-requests {:logger #ig/ref :duct/logger},
 :duct.middleware.web/defaults {:params {:urlencoded true,
                                         :multipart true,
                                         :nested true,
                                         :keywordize true},
                                :cookies true,
                                :session {:flash true,
                                          :cookie-attrs {:http-only true,
                                                         :same-site :strict}},
                                :security {:anti-forgery true,
                                           :xss-protection {:enable? true,
                                                            :mode :block},
                                           :frame-options :sameorigin,
                                           :content-type-options :nosniff},
                                :static {:resources ["duct/module/web/public"
                                                     "smallshop/public"]},
                                :responses {:not-modified-responses true,
                                            :absolute-redirects true,
                                            :content-types true,
                                            :default-charset "utf-8"}},
 :duct.server.http/jetty {:port 3000,
                          :handler #ig/ref :duct.handler/root,
                          :logger #ig/ref :duct/logger},
 :duct.database.sql/hikaricp {:jdbc-url nil,
                              :logger #ig/ref :duct/logger,
                              :connection-uri "jdbc:sqlite:db/dev.sqlite"},
 :duct.handler.static/internal-server-error {:headers {"Content-Type" "application/json"},
                                             :body #duct/resource "duct/module/web/errors/500.json"},
 :duct.middleware.web/hide-errors {:error-handler #ig/ref :duct.handler.static/internal-server-error},
 :duct.logger.timbre/spit {:fname "logs/dev.log"},
 :duct.middleware.web/log-errors {:logger #ig/ref :duct/logger},
 :duct.handler/root {:router #ig/ref :duct/router,
                     :middleware [#ig/ref :duct.middleware.web/not-found
                                  #ig/ref :duct.middleware.web/format
                                  #ig/ref :duct.middleware.web/defaults
                                  #ig/ref :duct.middleware.web/log-requests
                                  #ig/ref :duct.middleware.web/log-errors
                                  #ig/ref :duct.middleware.web/stacktrace
                                  #ig/ref :duct.middleware.web/webjars]},
 :duct.handler.static/not-found {:headers {"Content-Type" "text/html; charset=UTF-8"},
                                 :body #duct/resource "duct/module/web/errors/404.html"},
 :duct.migrator/ragtime {:database #ig/ref :duct.database/sql,
                         :strategy :rebase,
                         :logger #ig/ref :duct/logger,
                         :migrations []},
 :duct.middleware.web/webjars {},
 :smallshop.middleware/common {},
 :duct.middleware.web/not-found {:error-handler #ig/ref :duct.handler.static/not-found},
 :smallshop.handler/inventory {},
 :duct.core/environment :development,
 :duct.middleware.web/stacktrace {},
 :duct.handler.static/bad-request {:headers {"Content-Type" "text/html; charset=UTF-8"},
                                   :body #duct/resource "duct/module/web/errors/400.html"},
 :smallshop.handler/welcome {},
 :duct.core/project-ns smallshop}
~~~
