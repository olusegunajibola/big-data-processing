# estimated document count
db.users.estimatedDocumentCount()

# We can examine the contents of one of the documents by running 
db.users.findOne()
{
  _id: ObjectId("578ffa8e7eb9513f4f55a935"),
  user_name: 'koteras',
  retweet_count: 0,
  tweet_followers_count: 461,
  source: '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>',
  coordinates: null,
  tweet_mentioned_count: 1,
  tweet_ID: '755891629932675072',
  tweet_text: 'RT @ochocinco: I beat them all for 10 straight hours #FIFA16KING  https://t.co/BFnV6jfkBL',
  user: {
    CreatedAt: ISODate("2011-12-27T09:04:01.000Z"),
    FavouritesCount: 5223,
    FollowersCount: 461,
    FriendsCount: 619,
    UserId: 447818090,
    Location: '501'
  }
}

#  Query 1: How many tweets have location not null?
db.users.estimatedDocumentCount() - db.users.find( {'user.Location': null }).count()

# Query 2: How many people have more followers than friends?
db.users.find({$where :"this.user.FollowersCount > this.user.FriendsCount"}).count()

# Query 3: Return text of tweets which have the string "http://" ?
db.users.find({tweet_text: /http:/})

# Query 4: Return all the tweets which contain text "England" but not "UEFA" ?
db.users.find({$text:{$search : "England -UEFA"}})

# Query 5: Get all the tweets from the location "Ireland" and contains the string "UEFA"? 
db.users.find({$and :[  {tweet_text : /UEFA/}, { 'user.Location' : "Ireland" }]})
db.users.find({$and :[  {tweet_text : /UEFA/}, { 'user.Location' : "Ireland" }]}).count()

#Exporting Data from MongoDB to a CSV File - this is done on shell not mongosh
mongoexport --port=27017 --db=sample --collection=users --out=football_tweets.csv
# https://linuxhint.com/mongodb-export-all-collections/

https://github.com/taha7ussein007/Coursera_Bigdata_UCSD/blob/master/Big%20Data%20Integration%20and%20Processing/soccer-tweet-analysis.ipynb

