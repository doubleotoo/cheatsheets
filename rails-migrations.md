title: Rails migrations
-------

### Run migrations

    $ rake db:migrate

### Migrations

    create_table :users do |t|
      t.string :name
      t.text   :description

      t.primary_key :id
      t.string      :title
      t.text        :description
      t.integer     :games_count
      t.float       :lol
      t.decimal     :price
      t.decimal     :price, :precision => 2, :scale => 10
      t.datetime    :expiration
      t.timestamp   :time_in
      t.time        :time_in
      t.date        :expiry
      t.binary      :image_data
      t.boolean     :is_admin
    end

    # Options:
      :null (boolean)
      :limit (integer)
      :default

### Operations

    create_table
    change_table
    drop_table
    add_column
    change_column
    rename_column
    remove_column
    add_index
    remove_index

### Associations
    
    t.references :category   # kinda same as t.integer :category_id

    # Can have different types
    t.references :category, polymorphic: true

### Add/remove columns
  
    $ rails generate migration RemovePartNumberFromProducts part_number:string

    class RemovePartNumberFromProducts < ActiveRecord::Migration
      def up
        remove_column :products, :part_number
      end
     
      def down
        add_column :products, :part_number, :string
      end
    end

### Indices

    # Simple
    add_index :suppliers, :name

    # Unique
    add_index :accounts, [:branch_id, :party_id], :unique => true

    # Named (:name => ...)
    add_index :accounts, [:branch_id, :party_id], :unique => true, :name => "by_branch_party"

    # Length
    add_index :accounts, :name, :name => ‘by_name’, :length => 10
    add_index :accounts, [:name, :surname], :name => ‘by_name_surname’,
      :length => {
        :name => 10,
        :surname => 15
      }

    # Sort order (no MySQL support)
    add_index :accounts, [:branch_id, :party_id, :surname],
      :order => {:branch_id => :desc, :part_id => :asc}

### References

 * http://apidock.com/rails/ActiveRecord/ConnectionAdapters/SchemaStatements/add_index
