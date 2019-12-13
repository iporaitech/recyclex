# Recyclex

**JUST OUTLINING SOME IDEAS YET**

1. Use string :id with type encoded (like Relay Global ID), or
2. Use tuple {:id, type}, where id is integer and type is string representing the record type

## Install

`{:recyclex, "~> 0.1.0"}`

## Ecto migrations

1. Create migration `CreateRecycleBin`
2. Migrate

## Absinthe GraphQL Macros

```elixir
require Recyclex.GraphQL

# Add a :recycle_bin connection field / and connection (?)
Recyclex.GraphQL.connection_field()
connection(node_type: :recycle_bin_item)

# Add mutations
Recyclex.GraphQL.move_to_trash_mutation()
Recyclex.GraphQL.restore_mutation()
Recyclex.GraphQL.delete_permanent_mutation()

# Add node object :recycle_bin_item
Recyclex.GraphQL.node_object()

# Add pattern to resolve :recycle_bin_item to node interface
%RecycleBin.Item{}, _ ->
  :recycle_bin_item

# node field resolve (?)
```

## Backend functions

**Move a record to trash**

```elixir
Recyclex.move_to_trash(record OR global_id (?))
```

This would need record changeset, e.g.:

```elixir
person
|> Person.delete_changeset()
|> delete_and_insert_into_bin(global_id)
```

Restore a record from trash

```elixir
Recyclex.restore_from_trash(global_id OR {id, type})
```

View a record in the trash

```elixir
# TODO: How to use maps instead of deriving Jason.Encoder protocol for each Ecto schema
get(global_id)
```

Delete record permanently

```elixir
Recyclex.delete_permanent(record or global_id, or {id, type})
```

Do we need Dataloader functions?

```elixir
data()
query(queryalble)
```

```
