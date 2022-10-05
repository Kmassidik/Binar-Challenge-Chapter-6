sequelize model:generate --name UserGames --attributes username:string,password:string,role:string
sequelize model:generate --name UserGameBiodata --attributes fullname:string,age:integer
sequelize model:generate --name UserGameHistories --attributes user:string,com:string,result:string

please add this
UserGameId:{
    type: Sequelize.INTEGER,
    references:{
        model:{
            tableName:"UserGames"
        },
        key:'id',
        onDelete: 'CASCADE',
        onUpdate: 'CASCADE'
    }
},

at your (number)-create-user-game-biodata,(number )-create-user-game-histories migration.
it's make columns FK at your table.

UserGameBiodata.belongsTo(models.UserGames) on static associate(models) at usergamebiodata.js
UserGameHistories.belongsTo(models.UserGames) on static associate(models) at usergamehistories.js
UserGames.hasOne(models.UserGameBiodata), UserGames.hasOne(models.UserGameHistories) on static associate(models) at usergames.js